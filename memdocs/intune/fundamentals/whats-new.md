---
title: Nyheter i Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Ta reda på vad som är nytt i Intune Azure-portalen
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/24/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 791ed23f-bd13-4ef0-a3dd-cd2d7332c5cc
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: aa6839cef79623b456cd31eec6b894eae7687de3
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820280"
---
# <a name="whats-new-in-microsoft-intune"></a>Nyheter i Microsoft Intune

Lär dig mer om nyheter i Microsoft Intune varje vecka i [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431). Du kan också hitta [viktiga meddelanden](#notices), [tidigare versioner](whats-new-archive.md) och information om [hur uppdateringar av Intune-tjänsten släpps](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728). 

> [!Note]
> Varje [månadsuppdatering](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728) kan ta upp till tre dagar att distribuera och sker i följande ordning:
>
> - Dag 1: Asien och stillahavsområdet
> - Dag 2: Europa, Mellanöstern och Afrika
> - Dag 3: Nordamerika
> - Dag 4+: Intune för myndigheter
>
> Vissa funktioner kan distribueras över flera veckor och kanske inte är tillgängliga för alla kunder den första veckan.
>
> Titta närmare på sidan [Under utveckling ](in-development.md) för en lista över kommande funktioner i en version.

**RSS-feed**: Håll dig informerad när den här sidan uppdateras genom att kopiera och klistra in följande webbadress i feed-läsaren: `https://docs.microsoft.com/api/search/rss?search=%22What%27s+new+in+microsoft+intune%3F+-+Azure%22&locale=en-us`

<!-- Common categories:  
### App management
### Device configuration
### Device enrollment
### Device management
### Device security
### Intune apps
### Monitor and troubleshoot
### Role-based access control
### Scripts

<!-- ########################## -->
## <a name="Week-of-August-31-2020"></a>Veckan den 31 Augusti 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name=" Device-configuration"></a>Enhetskonfiguration

#### <a name="New-version-of-the-PFX-Certificate-Connector-and-changes-for-PKCS-certificate-profile-support--4839686----"></a>En ny version av PFX Certificat Connector och ändringar för PKCS certificat profil support <!--4839686-->

- Vi har släppt en ny version av PFX Certificat Connectorn, version 6.2008.60.607. I denna nya version:

- Support för PKCS certificat profiler på alla supportade plattformar förutom Windows 8.1

Vi har konsoliderat all PCKS support i PFX Certificat Connectorn. Detta betyder att, om du inte använder SCEP i din miljö, och du inte använder NDES för andra syften, kan du ta bort Microsoft Certificat Connector och avinstallera NDES i din miljö.

- Microsoft Certificat Connectors funktionallitet har inte tagits bort, du kan fortsätta använda den för support av PKCS certificat profiler.
- Support för certificat revokering i Outlook S/MIME
- Kräver .NET Framework 4.7.2

För mer information om certifikat connectorn, samt en versions historik för båda certificat connectorerna, se [Certificate connectors](../protect/certificate-connectors.md)

<!-- ########################## -->
## <a name="week-of-august-24-2020-2008-service-release"></a>Veckan den 24 augusti 2020 (2008 Service Release)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Apphantering

#### <a name="associated-licenses-revoked-before-deletion-of-apple-vpp-token--6195322----"></a>Tillhörande licenser återkallades innan en Apple VPP-token togs bort<!--6195322  -->
När du tar bort en Apple VPP-token i Microsoft Endpoint Manager så återkallas alla Intune-tilldelade licenser som är kopplade till denna token automatiskt innan token tas bort.

#### <a name="improvement-to-update-device-settings-page-in-company-portal-app-for-android-to-shows-descriptions----7414768-wnstaged---"></a>Förbättring av visning av beskrivningar på sidan Uppdatera enhetsinställningar i företagsportalappen för Android <!-- 7414768 wnstaged -->
I företagsportalappen på Android-enheter visar sidan **Uppdatera enhetsinställningar** de inställningar som behöver uppdateras för efterlevnad. Användare expanderar problemet för att visa mer information och ser då knappen **Lös**.

Den här användarupplevelsen har förbättrats. De visade inställningarna utökas som standard så att beskrivningen och knappen **Lös** visas om så är tillämpligt. Tidigare minimerades problemen som standard. Det nya standardbeteendet minskar antalet klick, så att användarna kan lösa problem snabbare.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Enhetskonfiguration

#### <a name="use-netmotion-as-a-vpn-connection-type-for-iosipados-and-macos-devices---1333631-----"></a>Använd NetMotion som VPN-anslutningstyp för iOS/iPad- och macOS-enheter<!-- 1333631   -->
När du skapar en VPN-profil är NetMotion tillgängligt som en VPN-anslutningstyp (**Enheter** > **Enhetskonfiguration** > **Skapa profil** > **iOS/iPad** eller **macOS** för plattform > **VPN-** för profil > **NetMotion** för anslutningstyp).

Mer information om VPN-profiler i Intune finns i [Skapa VPN-profiler för att ansluta till VPN-servrar](../configuration/vpn-settings-configure.md).

Gäller för:
- iOS/iPadOS
- macOS

#### <a name="more-protected-extensible-authentication-protocol-peap-options-for-windows-10-wi-fi-profiles---3805024----"></a>Fler PEAP-alternativ (Protected Extensible Authentication Protocol) för Windows 10 Wi-Fi-profiler<!-- 3805024  -->
På Windows 10-enheter kan du skapa Wi-Fi-profiler med EAP (Extensible Authentication Protocol) för att autentisera Wi-Fi-anslutningar (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **Windows 10 och senare** som plattform > **Wi-Fi** som profil > **Företag**).

När du väljer skyddad EAP (PEAP) finns det nya tillgängliga inställningar:
- **Utför serververifiering i PEAP fas 1**: I fas 1 av PEAP-förhandlingen verifieras servern av certifikatvalideringen.
  - **Inaktivera användaruppmaningar om att verifiera servern i PEAP fas 1**: I PEAP-förhandlingsfas 1 visas inte uppmaningar som ber användare att auktorisera nya PEAP-servrar för betrodda certifikatutfärdare.
- **Kräv kryptografisk bindning**: Förhindrar anslutningar till PEAP-servrar som inte använder krypteringsbindning under PEAP-förhandlingen.

Om du vill se de inställningar som du kan konfigurera går du tilll [Lägga till Wi-Fi-inställningar för enheter med Windows 10 och senare](../configuration/wi-fi-settings-windows.md).

Gäller för: 
- Windows 10 och senare

#### <a name="configure-the-macos-microsoft-enterprise-sso-plug-in---5627576--idstaged---"></a>Konfigurera macOS Microsoft Enterprise SSO-plugin-programmet<!-- 5627576  idstaged -->
Microsoft Azure AD-teamet skapade en app för omdirigering med enkel inloggning som gör att användare med macOS 10.15+ kan få åtkomst till Microsoft-appar, organisationsappar och webbplatser som stöder Apples SSO-funktion och autentisera med Azure AD. Med Microsoft Enterprises SSO-tillägget kan du konfigurera SSO-tillägget med den nya typen av Microsoft Azure AD-apptillägg (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **macOS** för plattform > **Enhetsfunktioner** > för profil > **Apptillägg för enkel inloggning** > Typ av SSO-apptillägg > **Microsoft Azure AD**).

För att få enkel inloggning med Microsoft Azure AD SSO-apptilläggstypen måste användarna installera och logga in på företagsportalsappen på sina macOS-enheter. 

Mer information om macOS-apptillägg för enkel inloggning finns i [Apptillägg för enkel inloggning](../configuration/device-features-configure.md#single-sign-on-app-extension).

Gäller för:
- macOS 10.15 och senare

#### <a name="prevent-users-from-unlocking-android-enterprise-work-profile-devices-using-face-and-iris-scanning--6069759-idmiss---"></a>Förhindra att användare låser upp Android Enterprise-enheter med arbetsprofil med ansikts-och irisigenkänning<!--6069759 idmiss -->
Du kan nu förhindra användare från att använda ansikts- eller irisigenkänning för att låsa upp sina enheter som hanteras med arbetsprofil, antingen på enhetsnivå eller på arbetsprofilnivå. Detta kan anges i **Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **Android Enterprise** för plattform > **Arbetsprofil > Enhetsbegränsningar** för profil > avsnitten **Arbetsprofilinställningar** och **Lösenord**.

Mer information finns i [Enhetsinställningarna för Android Enterprise tillåter eller begränsar funktioner med hjälp av Intune](../configuration/device-restrictions-android-for-work.md#work-profile-only).

Gäller för: 
- Android Enterprise-arbetsprofil

#### <a name="use-sso-app-extensions-on-more-iosipados-apps-with-the-microsoft-enterprise-sso-plug-in---7369991----"></a>Använd SSO-apptillägg på fler iOS/iPad-appar med Microsoft Enterprise SSO-plugin-programmet<!-- 7369991  -->
[Microsoft Enterprise SSO-plugin-programmet för Apple-enheter](https://docs.microsoft.com/azure/active-directory/develop/apple-sso-plugin) kan användas med alla appar som stöder SSO-apptillägg. I Intune innebär den här funktionen att plugin-programmet fungerar med mobila iOS/iPad-appar som inte använder Microsoft Authentication Library (MSAL) för Apple-enheter. Apparna behöver inte använda MSAL, men de måste autentiseras med Azure AD-slutpunkter.

Konfigurera dina iOS/iPad-appar så att de kan använda SSO med plugin-programmet genom att lägga till appaketidentifierarna i en iOS/iPad-konfigurationsprofil (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **iOS/iPad** för plattform > **Enhetsfunktioner** för profil > **Apptillägg för enkel inloggning** > **Microsoft Azure AD** för SSO-apptilläggstyp > **Appakets-ID:n**).

Om du vill se de aktuella inställningarna för SSO-tillägg som du kan konfigurera, så gå till [Enkel inloggning för apptillägg](../configuration/ios-device-features-settings.md#single-sign-on-app-extension).

Gäller för:
- iOS/iPadOS

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Enhetssäkerhet

#### <a name="deploy-endpoint-security-antivirus-policy-to-tenant-attached-devices-preview---5475441----"></a>Distribuera antivirusprincipen för slutpunktssäkerhet till klientanslutna enheter (förhandsvisning)<!-- 5475441  -->
Som förhandsversion kan du distribuera [principer för antivirus](../protect/endpoint-security-antivirus-policy.md) för slutpunktssäkerhet till enheter som du hanterar med Configuration Manager. I det här scenariot måste du konfigurera en klientanslutning mellan en version av Configuration Manager som stöds och din Intune-prenumeration. Följande versioner av Configuration Manager stöds:

- Aktuell gren för Configuration Manager 2006

Mer information finns i [Krav för Intune-slutpunktens säkerhetsprinciper](../protect/tenant-attach-intune.md#specific-requirements-for-intune-endpoint-security-policies) som stöd för klientanslutning.

#### <a name="changes-for-endpoint-security-antivirus-policy-exclusions--5583940-6018119------"></a>Ändringar av undantag för antiviruspolicyn för slutpunktssäkerhet<!--5583940, 6018119    -->
Vi har presenterat två ändringar för att hantera listorna för Microsoft Defender Antivirus-undantag som du kan konfigurera som en del av en [Endpoint Security-princip för antivirus](../protect/endpoint-security-antivirus-policy.md). Ändringarna hjälper dig att förhindra konflikter mellan olika principer och lösa konflikter i undantagslistorna som kan förekomma i dina tidigare distribuerade principer.

Båda ändringarna tillämpas på principinställningar för följande [Microsoft Defender Antivirus Configuration Service Providers](../protect/antivirus-microsoft-defender-settings-windows.md#microsoft-defender-antivirus-exclusions) (CSP:er):

- Defender/ExcludedPaths
- Defender/ExcludedExtensions
- Defender/ExcludedProcesses

Ändringarna är:

- Ny profiltyp: **Microsoft Defender Antivirus-undantag** – Använd den här nya profiltypen för Windows 10 och senare för att definiera en princip som bara fokuserar på antivirusundantag. Den här profilen kan hjälpa dig att förenkla hanteringen av dina undantagslistor genom att de skiljs från andra principkonfigurationer.

  Undantagen som du kan konfigurera omfattar Defender-*processer*, *filnamnstillägg* och *filer* och *mappar* som du inte vill att Microsoft Defender ska genomsöka.

- **Principsammanslagning** – Intune sammanfogar nu listan över undantag som du har definierat i separata profiler till en enda lista över undantag som ska gälla för varje enhet eller användare. När du exempelvis fokuserar på en användare med tre separata principer, så slås undantagslistorna från dessa tre principer samman till en enda stor uppsättning av *Microsoft Defender Antivirus-undantag* som sedan tillämpas på användaren.


<!-- ########################## -->
## <a name="week-of-august-17-2020"></a>Den vecka som börjar 17 augusti 2020

### <a name="intune-apps"></a>Intune-appar

#### <a name="custom-brand-image-now-displayed-in-the-windows-company-portal-profile-page---4280187---"></a>Anpassad varumärkesavbildning visas nu på Windows Företagsportal-profilsidan<!-- 4280187 -->
Som Microsoft Intune-administratör kan du ladda upp en anpassad varumärkesbild som visas som bakgrundsbild på användarens profilsida i Windows-företagsportalappen. Mer information finns i [Anpassa Intune Företagsportal-appar, företagsportalens webbplats och Intune-appen](../apps/company-portal-app.md#branding).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Apphantering

#### <a name="the-company-portal-adds-configuration-manager-application-support---4297660---"></a>Företagsportalen lägger till stöd för Konfigurationshanterarprogram<!-- 4297660 -->
Företagsportalen stöder nu Konfigurationshanterarprogram. Med den här funktionen kan slutanvändare se både program från Konfigurationshanteraren och sådana som distribuerats av Intune i Företagsportalen för samhanterade kunder. Det här stödet hjälper administratörer att konsolidera sina olika portalmiljöer för slutanvändare. Mer information finns i [Använd Företagsportalappen på samhanterade enheter](/mem/configmgr/comanage/company-portal). 

### <a name="device-security"></a>Enhetssäkerhet

#### <a name="set-device-compliance-state-from-third-party-mdm-providers---6361689---"></a>Ställ in enhetsefterlevnadstillståndet från MDM-tredjepartsleverantörer<!-- 6361689 -->

Intune stöder nu [MDM-lösningar från tredje part som källa för information om enhetsefterlevnad](../protect/device-compliance-partners.md). Efterlevnadsdata från tredje part kan användas för att genomdriva principer för villkorlig åtkomst för Microsoft 365 appar på iOS och Android genom integrering med Microsoft Intune.  Intune utvärderar kompatibilitetsinformation från tredjepartsleverantören för att avgöra om en enhet är betrodd och anger sedan attributen för villkorlig åtkomst i Azure AD.  Du fortsätter att skapa principer för villkorsstyrd åtkomst i Azure AD antingen från administrationscentret för Microsoft Endpoint Manager eller i Azure AD-portalen.

Följande MDM-leverantörer från tredje part stöds i den här versionen, som en offentlig förhandsversion:

- VMware WorkspaceONE UEM (tidigare känt som AirWatch)

*Den här uppdateringen distribueras till kunder globalt. Du bör se den här funktionen inom nästa vecka.*

<!-- ########################## -->
## <a name="week-of-august-10-2020"></a>Den vecka som börjar 10 augusti 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Enhetshantering

#### <a name="tenant-attach-install-an-application-from-the-admin-center----in7220536-cm6024389--"></a>Klientkoppling: Installera ett program från administrationscentret <!-- IN7220536 CM6024389-->
Du kan nu initiera en programinstallation i realtid för en klientorganisationsansluten enhet från administrationscentret för Microsoft Endpoint Manager. Mer information finns i [Anslut klientorganisation: Installera ett program från administrationscentret](../../configmgr/tenant-attach/applications.md).

<!-- ########################## -->
## <a name="week-of-july-27-2020"></a>Veckan som inleds med den 27 juli 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Övervaka och felsöka

#### <a name="power-bi-compliance-report-template-v20---636958---"></a>Mall för Power BI-efterlevnadsrapport V2.0<!-- 636958 -->
Med Power BI-mallar kan Power BI-partner skapa Power BI-appar med lite eller ingen kodning och distribuera dem till olika Power BI-kunder. Administratörer kan uppdatera mallversionen för Power BI-efterlevnadsrapporten från V1.0 till V2.0. V2.0 har en ny och bättre design samt ändringar av de beräkningar och data som visas i mallen. Mer information finns i [Ansluta till Data Warehouse med Power BI](../developer/reports-proc-get-a-link-powerbi.md) och [Uppdatera en mallapp](https://docs.microsoft.com/power-bi/service-template-apps-install-distribute#update-a-template-app). Dessutom kan du läsa blogginlägget om [den nya versionen av PowerBI-efterlevnadsrapporten med Intune Data Warehouse](https://aka.ms/new_compliance_report).

<!-- ########################## -->
## <a name="week-of-july-13-2020--2007-service-release"></a>Veckan som inleds den 13 juli 2020 (2007 Service Release)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Apphantering

#### <a name="exchange-on-premises-connector-support---7138486----"></a>Stöd för Exchange On-Premises Connector<!-- 7138486  -->
Intune tar bort stödet för funktionen Exchange On-premises Connector från Intune-tjänsten från och med version 2007 (juli). Befintliga kunder med aktiva anslutningsprogram kan fortsätta att använda funktionen. Nya kunder och befintliga kunder som inte har något aktivt anslutningsprogram kan inte längre skapa nya anslutningsprogram eller hantera EAS-enheter (Exchange ActiveSync) från Intune. Microsoft rekommenderar sådana kunder att skydda åtkomsten till Exchange lokalt med [HMA (modern hybridautentisering)](https://docs.microsoft.com/office365/enterprise/hybrid-modern-auth-overview). HMA ger tillgång till både Intune-appskyddspolicyer (kallas även MAM) och villkorsstyrd åtkomst via Outlook Mobile för Exchange lokalt.

#### <a name="smime-for-outlook-on-ios-and-android-devices-without-enrollment---6517155---"></a>S/MIME för Outlook på iOS- och Android-enheter utan registrering<!-- 6517155 -->
Nu kan du aktivera S/MIME för Outlook på iOS- och Android-enheter med en policy för appkonfiguration av hanterade appar. På så sätt kan du leverera policyn oavsett enhetens registreringsstatus. I [Administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), väljer du **Appar** > **Appkonfigurationsprinciper** > **Lägg till** > **Hanterade appar**. Dessutom kan du välja om du vill tillåta användare att ändra den här inställningen i Outlook. För automatisk distribution av S/MIME-certifikat till Outlook för iOS och Android måste enheten dock vara registrerad. Allmän information om S/MIME finns i [S/MIME-översikt om att signera och kryptera e-post i Intune](https://docs.microsoft.com/mem/intune/protect/certificates-s-mime-encryption-sign). Mer information om konfigurationsinställningarna för Outlook finns i [Konfigurationsinställningar för Microsoft Outlook](../apps/app-configuration-policies-outlook.md) och [Lägg till appkonfigurationsprinciper för hanterade appar utan enhetsregistrering](../apps/app-configuration-policies-managed-app.md). Information om S/MIME i Outlook för iOS och Android finns i [S/MIME-scenarier](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune#smime-scenarios) och [Konfigurationsnycklar – S/MIME-inställningar](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune#smime-settings). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Enhetskonfiguration

#### <a name="new-vpn-settings-for-windows-10-and-newer-devices---6602122-----"></a>Nya inställningar för Windows 10 och nyare enheter<!-- 6602122   -->

När du skapar en VPN-profil med IKEv2-anslutningstypen, så finns det nya inställningar som du kan konfigurera (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **Windows 10 och senare** för plattform > **VPN** för profil > **Bas-VPN**):

- **Enhetstunnel**: Tillåter enheter att automatiskt ansluta till VPN utan krav på interaktion från användarens sida, inklusive användarinloggning. Den här funktionen kräver att du aktiverar **Alltid på**, och använder **Datorcertifikat** som autentiseringsmetod.
- Kryptografisvitsinställningar: Konfigurera de algoritmer som används för att skydda IKE och underordnade säkerhetskopplingar, vilket gör det möjligt för dig att matcha klient- och serverinställningar.

Om du vill se vilka inställningar du kan konfigurera kan du gå till [Windows-enhetsinställningar för att lägga till VPN-anslutningar med Intune](../configuration/vpn-settings-windows-10.md).

Gäller för:

- Windows 10 och senare

#### <a name="configure-more-microsoft-launcher-settings-in-a-device-restrictions-profile-on-android-enterprise-devices-cobo---6285001----"></a>Konfigurera fler Microsoft Launcher-inställningar i en profil för enhetsbegränsningar på Android Enterprise-enheter (COBO)<!-- 6285001  -->

På fullständigt hanterade Android Enterprise-enheter kan du konfigurera fler Microsoft Launcher-inställningar med en profil för enhetsbegränsningar (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **Android Enterprise** för plattform > **Endast enhetsägare** > **Enhetsbegränsningar** > **Enhetsupplevelse** > **Fullständigt hanterad**). 

Om du vill se de här inställningarna går du till [Inställningar för Android Enterprise-enheter för att tillåta eller begränsa funktioner](../configuration/device-restrictions-android-for-work.md#device-experience).

Du kan också konfigurera inställningar för Microsoft Launcher med en [appkonfigurationsprofil](../apps/configure-microsoft-launcher.md).

Gäller för:

- Ägare av fullständigt hanterade Android Enterprise-enheter (COBO)

#### <a name="new-features-for-managed-home-screen-on-android-enterprise-device-owner-dedicated-devices-cosu---7414175-7133328-7133720-7134873-7135184---idstaged---"></a>Nya funktioner för hanterad Startskärm på Android Enterprise-enhetsägars dedikerade enheter (COSU)<!-- 7414175 7133328 7133720 7134873 7135184   idstaged -->

På Android Enterprise-enheter kan administratörer nu använda enhetskonfigurationsprofiler till att anpassa den hanterade startskärmen på dedikerade enheter som använder helskärmsläge med flera appar (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **Android Enterprise** för plattform > **Endast enhetsägare** > **Enhetsbegränsningar** för profil > **Enhetsupplevelse** > **Dedikerad enhet** > **Flera appar**).

Mer specifikt kan du:

- Anpassa ikoner, ändra skärmorientering och visa appmeddelanden i aktivitetsikoner <!--7414175-->
- Dölja genvägen till Hanterade inställningar <!--7133328-->
- Enklare åtkomst till felsökningsmenyn <!--7133720-->
- Skapa en lista med tillåtna Wi Fi-nätverk <!-- 7134873-->
- Få enklare åtkomst till enhetsinformationen <!-- 7135184-->

Mer information finns i [Inställningar för Android Enterprise-enheter för att tillåta eller begränsa funktioner](../configuration/device-restrictions-android-for-work.md) och i [den här bloggen](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-setup-microsoft-managed-home-screen-on-dedicated-devices/ba-p/1388060).

Gäller för:

- Android Enterprise-enhetsägare, dedikerade enheter (COBO)

#### <a name="administrative-templates-updated-for-microsoft-edge-84--7722068--"></a>Administrativa mallar uppdaterade för Microsoft Edge 84<!--7722068-->
De ADMX-inställningar som är tillgängliga för Microsoft Edge har uppdaterats. Nu kan slutanvändare konfigurera och distribuera nya ADMX-inställningar som lagts till i Edge 84. Mer information finns i [versionsanteckningarna för Edge 84](https://docs.microsoft.com/deployedge/microsoft-edge-relnote-stable-channel#policy-updates).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Enhetsregistrering

#### <a name="corporate-owned-personally-enabled-devices-preview--4442275----"></a>Företagsägda, personligt aktiverade enheter (förhandsversion)<!--4442275  -->
Intune har nu stöd för företagsägda Android Enterprise-enheter med en arbetsprofil för OS-versionerna Android 8 och senare. Företagsägda enheter med en arbetsprofil är ett av företagshanteringsscenarierna i Android Enterprise-lösningen. Det här scenariot gäller för enheter för enkelanvändare som är avsedda för företagsbruk och personligt bruk. Det här företagsägda, personligt aktiverade (COPE) scenariot erbjuder:

- containerisering av arbetsprofiler och personlig profiler
- kontroll på enhetsnivå för administratörer
- en garanti för slutanvändare att deras personliga data och program kommer att förbli privata

Den första offentliga förhandsversionen kommer att innehålla en delmängd av de funktioner som kommer att ingå i den allmänt tillgängliga versionen. Ytterligare funktioner kommer att läggas till löpande. De funktioner som är tillgängliga i den första förhandsgranskningen är:

- Registrering: Administratörer kan skapa flera registreringsprofiler med unika token som inte upphör att gälla. Enhetsregistrering kan göras via NFC, tokeninmatning, QR-kod, Zero Touch eller Knox Mobile-registrering.
- Enhetskonfiguration: En delmängd av de befintliga fullständigt hanterade och dedikerade enhetsinställningarna.
- Enhetsefterlevnad: Efterlevnadsprinciper som är tillgängliga för tillfället för fullständigt hanterade enheter.
- Enhetsåtgärder: Ta bort enheten (fabriksåterställning), starta om enheten och lås enheten.  
- Apphantering: Apptilldelningar, appkonfiguration och tillhörande rapporteringsfunktioner 
- Villkorlig åtkomst

Mer information om förhandsversionen av företagsägda med arbetsprofil finns i [supportbloggen](https://techcommunity.microsoft.com/t5/intune-customer-success/microsoft-announces-public-preview-for-android-enterprise/ba-p/1524325).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Enhetshantering

#### <a name="updates-to-the-remote-lock-action-for-macos-devices--7032805-----"></a>Uppdateringar av fjärrlåsningsåtgärden för macOS-enheter<!--7032805   -->
Här är några av ändringarna i fjärrlåsningsåtgärden för macOS-enheter:
- PIN-koden för återställning visas i 30 dagar innan den tas bort (i stället för sju dagar).
- Om en administratör har en andra webbläsare öppen och försöker att utlösa kommandot igen från en annan flik eller webbläsare låter Intune kommandot gå igenom. Rapporteringsstatusen anges dock som misslyckad snarare än att en ny PIN-kod skapas.
- Administratören kan inte utfärda ett nytt fjärrlåsningskommando om det tidigare kommandot fortfarande är väntande eller om enheten inte har checkat in igen.
Dessa ändringar är utformade för att förhindra att rätt PIN-kod skrivs över efter flera fjärrlåsnings-kommandon.

#### <a name="device-actions-report-differentiates-between-wipe-and-protected-wipe--7118901---"></a>Rapporten Enhetsåtgärder skiljer mellan rensning och skyddad radering<!--7118901 -->
Rapporten **Enhetsåtgärder** skiljer mellan åtgärderna för rensning och skyddad rensning. Om du vill se den här rapporten går du till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Enheter** > **Övervaka** > **Enhetsåtgärder** (under **Övrigt**).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Enhetssäkerhet

#### <a name="microsoft-defender-firewall-rule-migration-tool-preview---6423187-----"></a>Förhandsversion av migreringsverktyget för Microsoft Defender-brandväggsregler<!-- 6423187   -->
Vi jobbar på ett PowerShell-baserat verktyg i offentlig förhandsversion som ska migrera Windows Defender-brandväggsregler. När du installerar och kör verktyget skapas automatiskt policyer för brandväggsregler för slutpunktssäkerhet för Intune som baseras på Windows 10-klientens aktuella konfiguration. Mer information finns i [översikten över verktyget för migrering av brandväggsregler för slutpunktssäkerhet](../protect/endpoint-security-firewall-rule-tool.md).

#### <a name="endpoint-detection-and-response-policy-for-onboarding-tenant-attached-devices-to-mdatp-is-generally-available---7303816-----"></a>Policyn för slutpunktsidentifiering och svar för registrering av enheter anslutna till klientorganisationer till MDATP är allmänt tillgänglig<!-- 7303816   -->
Som ett led i arbetet med slutpunktssäkerheten i Intune är [policyerna för slutpunktsidentifiering och svar (EDR) för användning med enheter som hanteras av Configuration Manager](../protect/endpoint-security-edr-policy.md) inte längre i *förhandsversions* utan *allmänt tillgängliga*.

Om du vill använda EDR-policyn för enheter med en version av Configuration Manager som stöds konfigurerar du [Anslutning till klientorganisation för Configuration Manager](../../configmgr/tenant-attach/device-sync-actions.md). När du konfigurerar anslutningen till klientorganisationen kan du aktivera EDR-policyer för att registrera enheter som hanteras av Configuration Manager i Microsoft Defender ATP (Advanced Threat Protection).

#### <a name="bluetooth-settings-are-available-in-device-control-profiles-for-endpoint-security-attack-surface-reduction-policy---7032084-----"></a>Bluetooth-inställningar är tillgängliga i profilen Enhetskontroll för Endpoint Security-policyn Minska attackytan <!--7032084   -->
Vi har lagt till inställningar för att hantera Bluetooth på Windows 10-enheter i [profilen Enhetskontroll](../protect/endpoint-security-asr-profile-settings.md#device-control-profile) för *Endpoint Security-policyn Minska attackytan*.  Det här är samma inställningar som de som är tillgängliga i profilen Enhetsbegränsningar för *Enhetskonfiguration*.

#### <a name="manage-source-locations-for-definition-updates-with-endpoint-security-antivirus-policy-for-windows-10-devices---6347801-----"></a>Hantera källplatser för definitionsuppdateringar med Endpoint Security Antivirus-principen för Windows 10-enheter<!-- 6347801   -->  
Vi har lagt till två nya inställningar i kategorin *Uppdateringar* för [Endpoint Security-policyn Antivirus för Windows 10-enheter](../protect/antivirus-microsoft-defender-settings-windows.md#updates) som kan hjälpa dig att hantera hur enheter hämtar uppdaterade definitioner:

- *Ange filresurser för nedladdning av definitionsuppdateringar*
- *Ange källordning för nedladdning av definitionsuppdateringar*

Med de nya inställningarna kan du lägga till UNC-filresurser som källplatser för nedladdning av definitionsuppdateringar och definiera i vilken ordning olika källplatser kontaktas.

#### <a name="improved-security-baselines-node---7433136------"></a>Förbättringar av säkerhetsbaslinjenoden<!-- 7433136    -->
Vi har gjort några ändringar för att göra [säkerhetsbaslinjenoden](../protect/security-baselines.md) mer användbar i administrationscentret för Microsoft Endpoint Manager. Nu när du går vidare till **Endpoint Security** > **Säkerhetsbaslinjer** och väljer en typ av säkerhetsbaslinje som MDM Security Baseline visas fönstret **Profiler**. I fönstret Profiler ser du de profiler du har skapat för den aktuella baslinjetypen.  Tidigare såg du fönstret Översikt i konsolen, med en aggregerad datasamling som inte alltid matchade informationen i rapporterna för enskilda profiler.

Du kan fortfarande välja en profil att visa mer information om i fönstret Profiler, om du vill se profilens egenskaper eller olika rapporter som är tillgängliga under *Övervaka*.  På samma nivå som Profiler kan du också fortfarande välja **Versioner** om du vill visa en eller flera versioner av den profiltyp du har distribuerat. När du visar mer information om en version får du också tillgång till rapporter som liknar profilrapporterna. 

#### <a name="derived-credentials-support-for-windows---4886090-----"></a>Stöd för härledda autentiseringsuppgifter i Windows<!-- 4886090   -->
Nu kan du använda härledda autentiseringsuppgifter för dina Windows-enheter. Det här utökar det befintliga stödet för iOS/iPad och Android, och blir tillgängligt för samma härledda leverantörer av autentiseringsuppgifter:
- Entrust Datacard
- Intercede
- DISA Purebred

I stödet för Windows ingår att du kan använda härledda autentiseringsuppgifter till att autentisera för Wi-Fi- eller VPN-profiler. För Windows-enheter utfärdas härledda autentiseringsuppgifter från den klientapp som tillhandahålls av den leverantör du använder.

#### <a name="manage-filevault-encryption-for-devices-that-were-encrypted-by-the-device-user-and-not-by-intune--5239424----"></a>Hantera FileVault-kryptering för enheter som enhetsanvändaren och inte Intune har krypterat<!--5239424  -->
Intune kan nu [ta över hanteringen av FileVault-diskkryptering på macOS-enheter som enhetsanvändaren har krypterat](../protect/encrypt-devices-filevault.md#assume-management-of-filevault-on-previously-encrypted-devices).  Det här scenariot har följande förutsättningar:
- Enheten måste ta emot diskkrypteringspolicyn som aktiverar FileVault från Intune.
- Enhetsanvändaren måste använda Företagsportal-webbplatsen till att ladda upp den personliga återställningsnyckeln för den krypterade enheten till Intune. För att ladda upp nyckeln väljer användaren alternativet *Lagra återställningsnyckel* för den krypterade macOS-enheten.

När användaren har laddat upp återställningsnyckeln roterar Intune nyckeln för att bekräfta att den är giltig. Intune kan nu hantera nyckeln och krypteringen som om en policy användes till att kryptera enheten direkt. Om en användare behöver återställa sin enhet kan de komma åt återställningsnyckeln från valfri enhet från följande platser:   
- Företagsportalens webbplats
- Appen Företagsportal i iOS/iPadOS 
- Apen Företagsportal i Android
- Intune-appen

#### <a name="hide-the-personal-recovery-key-from-a-device-user-during-macos-filevault-disk-encryption----5475632--"></a>Dölj den personliga återställningsnyckeln från en enhetsanvändare vid diskkrypteringen i macOS FileVault<!--  5475632-->
När du använder en policy för slutpunktssäkerhet till att konfigurera FileVault-diskkryptering i macOS använder du inställningen [**Dölj återställningsnyckel**](../protect/endpoint-security-disk-encryption-profile-settings.md#filevault) till att hindra att den *personliga återställningsnyckeln* visas för enhetsanvändaren medan enheten krypteras. Genom att dölja nyckeln under krypteringen kan du hålla den säker eftersom användarna inte kan skriva ned den medan de väntar på att enheten ska krypteras. 

Om enheten behöver återställas senare kan användaren alltid använda valfri enhet till att visa sin personliga återställningsnyckel via Företagsportal-webbplatsen, appen Företagsportal i iOS/iPadOS, appen Företagsportal i Android eller Intune-appen.

#### <a name="improved-view-of-security-baseline-details-for-devices---5536846----"></a>Förbättrad vy av säkerhetsbaslinjeinformation för enheter<!-- 5536846  -->
Nu kan du visa mer information om en enhet och se vilka inställningar för säkerhetsbaslinjer som används för enheten. Inställningarna visas i en enkel lista där du ser inställningskategori, inställningsnamn och status. Mer information finns i [Visa konfiguration av slutpunktssäkerhet per enhet](../protect/security-baselines-monitor.md#view-endpoint-security-configurations-per-device).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Övervaka och felsöka

#### <a name="device-compliance-logs-now-in-english--6014904----"></a>Enhetsefterlevnadsloggarna finns nu på engelska<!--6014904  -->
Intunes DeviceComplianceOrg-loggar hade tidigare bara uppräkningar för ComplianceState, OwnerType och DeviceHealthThreatLevel. Nu innehåller loggarna information på engelska i kolumnerna.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Rollbaserad åtkomstkontroll

#### <a name="assign-profile-and-update-profile-permission-changes--7177586-----"></a>Behörighetsändringar för Tilldela profil och Uppdatera profil<!--7177586   -->
Behörigheterna för rollbaserad åtkomstkontroll har ändrats för Tilldela profil och Uppdatera profil i flödet för automatisk enhetsregistrering:

Tilldela profil: Administratörer med den här behörigheten kan också tilldela profiler till tokens och tilldela en standardprofil till en token för ADE.

Uppdatera profil: Administratörer med den här behörigheten kan bara uppdatera befintliga profiler för ADE.

Om du vill se de här rollerna går du till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Klientadministration** > **Roller** > **Alla roller** > **Skapa** > **Behörigheter** > **Roller**.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="scripting"></a>Använda skript

#### <a name="additional-data-warehouse-v10-properties---6125732----"></a>Ytterligare egenskaper för Data Warehouse v 1.0<!-- 6125732  -->
Ytterligare egenskaper finns tillgängliga med Intune Data Warehouse v 1.0. Följande egenskaper exponeras nu via [enheter](../developer/reports-ref-devices.md#devices)-entiteten:
- `ethernetMacAddress` – den unika nätverksidentifieraren för den här enheten.
- `office365Version` – den version av Office 365 som är installerad på enheten.

Följande egenskaper är nu tillgängliga via [devicepropertyHistory](../developer/reports-ref-devices.md#devicepropertyhistories)-entiteten:
- `physicalMemoryInBytes` – fysiskt minne i bytes.
- `totalStorageSpaceInBytes` – Total lagringskapacitet i bytes.

Mer information finns i [Microsoft Intune-API:et Data Warehouse](../developer/reports-nav-intune-data-warehouse.md).

<!-- ########################## -->
## <a name="week-of-july-06-2020"></a>Vecka 28, 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Apphantering

#### <a name="update-to-device-icons-in-company-portal-and-intune-apps-on-android---6057023---"></a>Uppdatera till enhet-ikoner i Företagsportalen och Intune-appar på Android<!-- 6057023 -->
Vi uppdaterar enhetsikonerna i Företagsportalen och Intune-appar på Android-enheter för att skapa ett modernt utseende och att anpassa sig till designsystemet Microsoft Fluent. Relaterad information finns i [Uppdatera till ikoner i företagsportalappen för iOS/iPadOS och macOS](../fundamentals/whats-new-app-ui.md#update-to-icons-in-company-portal-app-for-iosipados-and-macos-). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Enhetsregistrering

#### <a name="ios-company-portal-will-support-apples-automated-device-enrollment-without-user-affinity---7282707---"></a>iOS Företagsportalen kommer att stödja Apples automatiserade enhetsregistrering utan användartillhörighet<!-- 7282707 --> 
iOS Företagsportalen kommer att stödjas på enheter som har registrerats med Apples automatiserade enhetsregistrering utan att kräva en tilldelad användare. En slutanvändare kan logga in på iOS Företagsportalen för att etablera sig själva som primär användare på en iOS/iPad-enhet som registrerats utan enhetstillhörighet. Mer information om automatiserad enhetsregistrering finns i [Registrera iOS/iPadOS-enheter automatiskt med Apples automatiska enhetsregistrering](../enrollment/device-enrollment-program-enroll-ios.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Enhetshantering

#### <a name="tenant-attach-configmgr-client-details-in-the-admin-center-preview---7552762---"></a>Klientkoppling: ConfigMgr-klientinformation i administrationscenter (förhandsversion)<!-- 7552762 -->

Du kan nu se information om ConfigMgr-klienter, inklusive samlingar, gränsgruppsmedlemskap och klientinformation i realtid för en specifik enhet i administrationscentret för Microsoft Endpoint Manager. Mer information finns i [Anslut klientorganisation: ConfigMgr-klientinformation i administrationscenter (förhandsversion)](../../configmgr/tenant-attach/client-details.md).

## <a name="week-of-june-22-2020"></a>Veckan som inleds med 22 juni 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Apphantering

#### <a name="newly-available-protected-apps-for-intune---7248952---"></a>Nyligen tillgängliga skyddade appar för Intune<!-- 7248952 -->
Följande skyddade appar är nu tillgängliga:
- BlueJeans-videokonferens
- Cisco Jabber för Intune
- Tableau Mobile för Intune
- ZERO för Intune

Mer information om skyddade appar finns i [Microsoft Intune-skyddade appar](../apps/apps-supported-intune-apps.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Övervaka och felsöka

#### <a name="use-endpoint-analytics-to-improve-user-productivity-and-reduce-it-support-costs---5653063---"></a>Använd slutpunktsanalys för att förbättra användarproduktiviteten och minska kostnader för IT-support<!-- 5653063 --> 
Den här funktionen kommer att lanseras under nästa vecka. Målet med slutpunktsanalys är att förbättra användarproduktiviteten och minska kostnader för IT-support genom att ge insikter om användarupplevelsen. Insikterna gör det möjligt för IT att optimera slutanvändarupplevelsen med proaktiv support och att identifiera regressioner i användarupplevelsen genom att bedöma användarpåverkan för konfigurationsändringar. Mer information finns i [förhandsversion](https://aka.ms/uea) för slutpunktsanalys.

#### <a name="proactively-remediate-end-user-device-issues-using-script-packages---5933328---"></a>Proaktivt åtgärda problem med slutanvändares enheter via skriptpaket<!-- 5933328 -->
Du kan skapa och köra skriptpaket på slutanvändares enheter för att proaktivt identifiera och åtgärda de vanligaste supportärendena i organisationen. Genom att distribuera skriptpaket kan du minska antalet supportsamtal. Välj om du vill skapa egna skriptpaket eller distribuera ett av skriptpaketen vi har skrivit och använder i vår miljö för att minska antalet supportärenden. Med Intune kan du se status för dina distribuerade skriptpaket och övervaka identifierings- och åtgärdsresultaten. Gå till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) och välj **Rapporter** > **Slutpunktsanalys** > **Proaktiva åtgärder**. Mer information finns i [Proaktiva åtgärder](https://aka.ms/uea_prs).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Enhetssäkerhet

#### <a name="use-microsoft-defender-atp-in-compliance-policies-for-android---4425686----"></a>Använd Microsoft Defender ATP i policyer för efterlevnad i Android<!-- 4425686  -->

Nu kan du använda Intune till att [registrera Android-enheter i Microsoft Defender Advanced Threat Protection](../protect/advanced-threat-protection-configure.md#onboard-devices) (Microsoft Defender ATP). När dina enheter har registrerats kan dina policyer för efterlevnad i Android använda signaler om *hotnivåer* från Microsoft Defender ATP. Det här är samma signaler som du tidigare kunnat använda för Windows 10-enheter.

#### <a name="configure-defender-atp-web-protection-for-android-devices---6185563----"></a>Konfigurera webbskydd i Defender ATP för Android-enheter<!-- 6185563  -->

När du använder Microsoft Defender Avancerat skydd (Microsoft Defender ATP) för Android-enheter kan du [konfigurera webbskyddet i Microsoft Defender ATP](../protect/advanced-threat-protection-manage-android.md) för att inaktivera nätfiskefunktionen eller förhindra att VPN-nätverket används vid genomsökningar.

Beroende på hur din Android-enhet är registrerad i Intune är följande alternativ tillgängliga:

- Android-enhetsadministratör – använd anpassade OMA-URI-inställningar till att inaktivera webbskyddsfunktionen eller inaktivera endast användningen av VPN vid genomsökningar.
- Android Enterprise-arbetsprofil – använd en appkonfigurationsprofil och Configuration Designer till att inaktivera alla webbskyddsfunktioner.

<!-- ########################## -->
## <a name="week-of-june-15-2020--2006-service-release"></a>Veckan som inleds den 15 juni 2020 (2006 Service Release)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Apphantering  

#### <a name="telecommunications-data-transfer-protection-for-managed-apps---6884491----"></a>Skydd för dataöverföring via telekommunikation för hanterade appar<!-- 6884491  -->
När ett hyperlänkat telefonnummer identifieras i en skyddad app kontrollerar Intune om det används någon skyddsprincip som tillåter att numret överförs till en uppringningsapp. Du kan välja hur du vill hantera den här typen av innehållsöverföring när den initieras från en policyhanterad app. När du skapar en appskyddspolicy i Microsoft Endpoint Manager väljer du ett alternativ för hanterade appar från **Skicka organisationsdata till andra appar** och väljer sedan ett alternativ från **Överför telekommunikationsdata till**. Mer information om den här dataskyddsinställningen finns i [Inställningar för Android-appskyddsprinciper i Microsoft Intune](../apps/app-protection-policy-settings-android.md) och [Inställningar för iOS-appskyddsprinciper](../apps/app-protection-policy-settings-ios.md). 

#### <a name="unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-company-portal---7414033----"></a>Enhetlig leverans av Azure AD Enterprise- och Office Online-program i Företagsportal<!-- 7414033  -->
I fönstret **Anpassning** i Intune kan du välja att **Dölja** eller **Visa** både **Azure AD Enterprise-program** och **Office Online-program** i Företagsportal. Slutanvändarna ser hela programkatalogen från den valda Microsoft-tjänsten. Som standard är **Dölj** valt för alla ytterligare appkällor. Den här funktionen börjar först gälla på Företagsportal-webbplatsen. Stödet för Windows-företagsportaler förväntas komma senare. Du hittar den här konfigurationsinställningen i [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) genom att välja **Administration av klientorganisation** > **Anpassning**. Mer information finns i [Anpassa Intune Företagsportal-appar, företagsportalens webbplats och Intune-appen](../apps/company-portal-app.md).

#### <a name="improvements-to-the-company-portal-for-macos-enrollment-experience---6444452----"></a>Förbättringar av registreringsfunktionen i macOS-företagsportalappen<!-- 6444452  -->
Företagsportalen för macOS-registrering har en enklare registreringsprocess som stämmer bättre överens med företagsportalen för iOS-registrering. Enhetsanvändarena ser:  
- Ett mer elegant användargränssnitt.  
- En förbättrad checklista för registrering.  
- Tydligare instruktioner för hur man registrerar sina enheter.  
- Förbättrade felsökningsalternativ.  

Mer information om företagsportalen finns i [Anpassa Intune-företagsportalappar, företagsportalens webbplats och Intune-appen](../apps/company-portal-app.md).

#### <a name="improvements-to-devices-page-of-iosipados-and-macos-company-portals---6055001---"></a>Förbättringar av sidan Enheter i företagsportalerna för ioS/iPad och macOS<!-- 6055001 -->
Vi har gjort ändringar på sidan **Enheter** i Företagsportal för att ge iOS/iPadOS- och Mac-användare en bättre upplevelse. Förutom att ge den ett modernare utseende har vi ordnat om enhetsinformationen i en enda kolumn med definierade avsnittsrubriker så att det blir lättare för användarna att se sin enhetsstatus. Dessutom har vi lagt till tydligare meddelanden och felsökningssteg för användare vars enheter inte uppfyller efterlevnadskraven. Mer information om Företagsportal finns i [Anpassa Intune-företagsportalappar, företagsportalens webbplats och Intune-appen](../apps/company-portal-app.md). Om du vill synkronisera en enhet manuellt kan du läsa i [Synkronisera din iOS-enhet manuellt](../user-help/sync-your-device-manually-ios.md).  

#### <a name="cloud-setting-for-iosipados-company-portal-app---7071303----"></a>Inställningen Moln för företagsportalappen i iOS/iPadOS<!-- 7071303  -->
Med den nya inställningen **Moln** i företagsportalen i iOS/iPad kan användarna dirigera om sin autentisering till lämpligt moln för organisationen. Som standard konfigureras inställningen som **Automatiskt**, vilket dirigerar autentiseringen mot molnet som automatiskt identifieras av användarens enhet. Om autentiseringen för organisationen måste dirigeras om mot ett annat moln än det som identifieras automatiskt (till exempel ett offentligt moln eller myndighetsmoln) kan användarna manuellt välja rätt moln genom att välja appen **Inställningar** > **Företagsportal** > **Moln**. Användarna bör bara ändra inställningen **Moln** från **Automatiskt** om de loggar in från en annan enhet och rätt moln inte identifieras automatiskt av enheten. 

#### <a name="duplicate-apple-vpp-tokens---7101606----"></a>Dubbletter av Apple VPP-token<!-- 7101606  -->
Apple VPP-token med samma **Tokenplats** markeras nu som **Dubbletter** och kan synkroniseras igen när dubblettoken har tagits bort. Du kan fortfarande tilldela och återkalla licenser för token som är markerade som dubbletter. Licenser för nya appar och böcker som köps kanske dock inte återspeglas när en token är markerade som dubblett. Om du vill hitta Apple VPP-token för din klientorganisation går du till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) och väljer **Administration av klientorganisation** > **Anslutningsprogram och token** > **Apple VPP-token**. Mer information om VPP-token finns i [Hantera iOS- och macOS-appar som köpts genom ett Apples volymköpsprogram med Microsoft Intune](../apps/vpp-apps-ios.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Enhetskonfiguration

#### <a name="add-multiple-root-certificates-for-eap-tls-authentication-in-wi-fi-profiles-on-macos-devices---2077871----"></a>Lägga till flera rotcertifikat för EAP-TLS-autentisering i Wi-Fi-profiler på macOS-enheter<!-- 2077871  -->

På macOS-enheter kan du skapa en Wi-Fi-profil och välja autentiseringstypen EAP (Extensible Authentication Protocol) (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **macOS** som plattform > **Wi-Fi** som profil > och Företag som **Wi-Fi-typ**).

När du ställer in **EAP-typ** på autentisering med **EAP-TLS**, **EAP-TTLS** eller **PEAP** kan du lägga till flera rotcertifikat. Tidigare kunde du bara lägga till ett rotcertifikat.

Mer information om vilka inställningar du kan konfigurera finns i [Lägga till Wi-Fi-inställningar för macOS-enheter i Microsoft Intune](../configuration/wi-fi-settings-macos.md).

Gäller för:
- macOS

#### <a name="use-pkcs-certificates-with-wi-fi-profiles-on-windows-10-and-newer-devices---3246388-----"></a>Använda PKCS-certifikat med Wi-Fi-profiler på enheter med Windows 10 och senare<!-- 3246388   -->
Du kan autentisera Wi-Fi-profiler i Windows med SCEP-certifikat (**Enhetskonfiguration** > **Profiler** > **Skapa profil** > **Windows 10 och senare** som plattform > **Wi-Fi** som profiltyp > **Företag** > **EAP-typ**). Nu kan du använda PKCS-certifikat med dina Wi-Fi-profiler i Windows. Med den här funktionen kan användarna autentisera Wi-Fi-profiler med hjälp av nya eller befintliga PKCS-certifikatprofiler i din klientorganisation. 

Mer information om vilka Wi-Fi-inställningar du kan konfigurera finns i [Lägga till Wi-Fi-inställningar för enheter med Windows 10 eller senare i Microsoft Intune](../configuration/wi-fi-settings-windows.md).

Gäller för:
- Windows 10 och senare

#### <a name="wired-network-device-configuration-profiles-for-macos-devices---3508686----"></a>Enhetskonfigurationsprofiler för fast nätverk för macOS-enheter<!-- 3508686  -->
Det finns en ny konfigurationsprofil för macOS-enheter tillgänglig som konfigurerar kabelanslutna nätverk (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **macOS** som plattform > **Kabelanslutet nätverk** som profil). Använd den här funktionen för att skapa 802.1 x-profiler för att hantera kabelanslutna nätverk och distribuera dessa kabelanslutna nätverk till dina macOS-enheter.

Mer information om den här funktionen finns i [Kabelanslutna nätverk på macOS-enheter](../configuration/wired-networks-configure.md).

Gäller för:
- macOS

#### <a name="use-microsoft-launcher-as-the-default-launcher-for-fully-managed-android-enterprise-devices---4927976-----"></a>Använd Microsoft Launcher som standardstartprogram för fullständigt hanterade Android Enterprise-enheter<!-- 4927976   -->
På Android Enterprise-ägarenheter kan du ställa in Microsoft Launcher som standardstartprogram för fullständigt hanterade enheter (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **Android Enterprise** för plattform > **Enhetsägare** > **Enhetsbegränsningar** för profil > **Enhetsupplevelse**). Om du vill konfigurera alla andra inställningar för Microsoft Launcher använder du [appkonfigurationsprinciper](../apps/configure-microsoft-launcher.md). 

Det finns också några andra UI-uppdateringar, inklusive **Dedikerade enheter** som har bytt namn till **Enhetsupplevelse**.

Om du vill se alla inställningar som du kan begränsa går du till [Inställningar för Android Enterprise-enheter för att tillåta eller begränsa funktioner med Intune](../configuration/device-restrictions-android-for-work.md). 

Gäller för:
- Ägare av fullständigt hanterade Android Enterprise-enheter (COBO)

#### <a name="use-autonomous-single-app-mode-settings-to-configure-the-ios-company-portal-app-to-be-a-sign-insign-out-app---7055619-----"></a>Använd inställningarna för Autonomt enappsläge när du ska konfigurera iOS-företagsportalen som en app för in- och utloggning<!-- 7055619   -->
På iOS/iPadOS-enheter kan du konfigurera att appar ska köras i autonomt enappsläge (ASAM). Nu har företagsportalappen stöd för ASAM och kan konfigureras som en ”logga in/logga ut”-app. I det här läget måste användare loggar in i företagsportalappen för att kunna använda andra appar och startknappen på enheten. När de loggar ut från appen Företagsportal återgår enheten till enappsläget och låser appen Företagsportal.

Om du vill konfigurera företagsportalen i ASAM-läge går du till **Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **iOS/iPadOS** som plattform > **Enhetsbegränsningar** som profil > **Autonomt enappsläge**.

Mer information finns i [Autonomt enappsläge (ASAM)](../configuration/device-restrictions-ios.md#autonomous-single-app-mode-asam) och [enappsläge](https://support.apple.com/guide/mdm/single-app-mode-mdm80a981/1/web/1) (öppnar Apples webbplats).

Gäller för:
- iOS/iPadOS

#### <a name="configure-content-caching-on-macos-devices---7106872-----"></a>Konfigurera cachelagring av innehåll på macOS-enheter<!-- 7106872   -->
På macOS-enheter kan du skapa en konfigurationsprofil som konfigurerar cachelagring av innehåll (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **macOS** för plattformen**Enhetsfunktioner** för profilen). Använd de här inställningarna om du vill ta bort cache, tillåta delad cache, ställa in en cachegräns för disken med mera.

Mer information om innehållscachelagring finns i [Innehållscachelagring](https://developer.apple.com/documentation/devicemanagement/contentcaching) (öppnar Apples webbplats).

Om du vill visa vilka inställningar du kan konfigurera går du till [Inställningar för macOS-enhetsfunktioner i Intune](../configuration/macos-device-features-settings.md).

Gäller för:
- macOS

#### <a name="add-new-schema-settings-and-search-for-existing-schema-settings-using-oemconfig-on-android-enterprise---6394386-----"></a>Lägg till nya schemainställningar och sök efter befintliga schemainställningar med OEMConfig på Android Enterprise<!-- 6394386   -->
I Intune kan du använda OEMConfig för att hantera inställningar för Android Enterprise-enheter (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **Android Enterprise** för plattformen > **OEMConfig** för profilen). När du använder **Configuration Designer** så visas egenskaperna i appens schema. I **Configuration Designer** kan du:

- Lägg till nya inställningar i appens schema.
- Sök efter nya och befintliga inställningar i appens schema.

Mer information om OEMConfig-profiler i Intune finns i [Använda och hantera Android Enterprise-enheter med OEMConfig i Microsoft Intune](../configuration/android-oem-configuration-overview.md).

Gäller för:
- Android enterprise

#### <a name="block-shared-ipad-temporary-sessions-on-shared-ipad-devices---6613794----"></a>Blockera delade tillfälliga iPad-sessioner på delade iPad-enheter<!-- 6613794  -->
I Intune finns det en ny inställning, **Blockera delade tillfälliga iPad-sessioner**, som blockerar tillfälliga sessioner på delade iPad-enheter (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **iOS/iPad** för plattform > **Enhetsbegränsningar** för profiltyp > **Delad iPad**). När detta har aktiverats kan slutanvändarna inte använda gästkontot. De måste logga in på enheten med sina hanterade Apple-ID:n och lösenord. 

Mer information finns i [Inställningar på iOS- och iPadOS-enheter för att tillåta eller begränsa funktioner](../configuration/device-restrictions-ios.md).

Gäller för:
- Delade iPad-enheter som kör iOS/iPad 13.4 och senare

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Enhetsregistrering

#### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344----"></a>VPN kan användas för att distribuera egna enheter (BYOD, Bring Your Own Device)<!--5015344  -->
Med den nya växlingsknappen **Hoppa över kontroll av domänanslutning** för Autopilot-profil kan du distribuera Hybrid Azure AD-anslutna enheter utan åtkomst till ditt företagsnätverk med hjälp av din egen Win32 VPN-klient från 3:e part. Om du vill se den nya växlingsknappen kan du gå till [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Enheter**  > **Windows** > **Windows-registrering** > **Distributionsprofiler** > **Skapa profil** > **Välkomstupplevelse (OOBE)** .

#### <a name="enrollment-status-page-profiles-can-be-set-to-device-groups--3952138---"></a>Profilerna för sidan för registreringsstatus kan tilldelas till enhetsgrupper<!--3952138 -->
Tidigare kunde endast användargrupper vara mål för profiler för sidan för registreringsstatus. Nu kan du även rikta in dem mot enhetsgrupper. Mer information finns i [Konfigurera en sida för registreringsstatus](../enrollment/windows-enrollment-status.md).

#### <a name="automated-device-enrollment-sync-errors---6988214---"></a>Synkroniseringsfel vid automatisk enhetsregistrering<!-- 6988214 -->
Nya fel rapporteras för iOS/iPad- och macOS-enheter, inklusive
- Ogiltiga tecken i telefonnumret eller om fältet är tomt. 
- Ogiltigt eller tomt konfigurationsnamn för profilen. 
- Ogiltigt/utgånget markörvärde eller saknad markör.
- Nekad eller förfallen token. 
- Avdelningsfältet i profilen är tomt eller för långt. 
- Apple kunde inte hitta profilen, och en ny måste skapas. 
- Antalet borttagna Apple Business Manager-enheter kommer att läggas till på översiktssidan, där dina enheters status visas.

#### <a name="shared-ipads-for-business--6367326-----"></a>Delat iPad for Business<!--6367326   -->
Du kan använda Intune och Apple Business Manager till att enkelt och säkert konfigurera delade iPad-enheter så att flera medarbetare kan dela enheter. Apples [Delad iPad](https://developer.apple.com/education/shared-ipad/) får en ny anpassad upplevelse för flera användare samtidigt som användardata bevaras. Med ett hanterat Apple-ID kan användare komma åt sina appar, data och inställningar efter att ha loggat in på en delad iPad i organisationen. Delad iPad fungerar med federerade identiteter.

Du ser den här funktionen genom att gå till [Administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Enheter** > **iOS** > **iOS-registrering** > **Registreringsprogramtoken** > **välj en token** > **Profiler** > **Skapa profil** > **iOS**. På sidan **Hanteringsinställningar** väljer du **Registrera utan användartillhörighet** så visas alternativet **Delad iPad**.

Kräver: iPad iPadOS 13.4 eller senare. Den här versionen innehåller stöd för tillfälliga sessioner med delad iPad så att användarna kan komma åt en enhet utan ett hanterat Apple-ID. Vid utloggning raderar enheten all användarinformation så att enheten omedelbart kan användas, vilket eliminerar behovet av enhetsrensning. 

#### <a name="updated-user-interface-for-apples-automated-device-enrollment--7430322---"></a>Uppdaterat användargränssnitt för Apples automatiserade enhetsregistrering<!--7430322 -->
Användargränssnittet har uppdaterats med bättre terminologi under bytet från Apples Programmet för enhetsregistrering till Automatisk enhetsregistrering.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Enhetshantering

#### <a name="device-remote-lock-pin-available-for-macos--7281557-----"></a>Nu är PIN-koder för fjärrlåsning tillgängliga för macOS-enheter<!--7281557   -->
Tillgängligheten för PIN-koder för fjärrlåsning av macOS-enheter utökas från 7 till 30 dagar.

#### <a name="change-primary-user-on-co-managed-devices--7319183----"></a>Ändra primär användare på samhanterade enheter<!--7319183  -->
Du kan ändra en enhets primära användare för samhanterade Windows-enheter. Mer information om hur du hittar och ändrar detta finns i [Hitta en Intune-enhets primära användare](../remote-actions/find-primary-user.md). Den här funktionen lanseras gradvis under de kommande veckorna.

#### <a name="setting-the-intune-primary-user-also-sets-the-azure-ad-owner-property--7319227---"></a>Om du anger en primär Intune-användare anges också egenskapen Azure AD Owner<!--7319227 -->
Den här nya funktionen ställer automatiskt in egenskapen Ägare på nyregistrerade Hybrid Azure AD-anslutna enheter samtidigt som den primära Intune-användaren anges. Mer information om den primär användare finns i [Hitta en Intune-enhets primära användare](../remote-actions/find-primary-user.md).

Detta är en ändring i registreringsprocessen och gäller endast nyligen registrerade enheter. För befintliga Hybrid Azure AD-anslutna enheter måste du uppdatera egenskapen för Azure AD-ägare manuellt. Om du vill göra detta kan du använda funktionen [Ändra primär användare](../remote-actions/find-primary-user.md#change-a-devices-primary-user) eller [ett skript](https://github.com/microsoftgraph/powershell-intune-samples/tree/master/ManagedDevices).

När Windows 10-enheter ansluts till Azure-katalogen för Hybrid Azure blir enhetens första användare den primära användaren i Endpoint Manager.  Användaren har för tillfället inte konfigurerats för motsvarande Azure AD-enhetsobjekt. Detta orsakar en inkonsekvens när du jämför egenskapen *ägare* från en Azure AD-portal med egenskapen *primär användare* i administrationscentret för Microsoft Endpoint Manager. Egenskapen Azure AD-ägare används för att skydda åtkomsten till BitLocker-återställningsnycklar. Egenskapen har inte fyllts i på Hybrid Azure AD-anslutna enheter. Den här begränsningen förhindrar konfiguration av självbetjäning av BitLocker-återställning från Azure AD. Denna kommande funktion löser den här begränsningen.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Enhetssäkerhet

#### <a name="hide-the-recovery-key-from-users-during-filevault-2-encryption-for-macos-devices---5459801----"></a>Dölj återställningsnyckeln från användare under FileVault 2-kryptering för macOS-enheter<!-- 5459801  -->
Vi har lagt till en ny inställning i *FileVault*-kategorin i mallen [macOS-slutpunktsskydd](../protect/endpoint-protection-macos.md#filevault): **Dölj återställningsnyckel**. Den här inställningen döljer den personliga nyckeln från slutanvändaren under FileVault 2-kryptering. 

Om du vill visa den personliga återställningsnyckeln för en krypterad macOS-enhet kan du gå till någon av följande platser och klicka på *Hämta återställningsnyckel* för macOS-enheten: 

- företagsportalappen i iOS/iPadOS
- Intune-appen
- Företagsportalswebbplatsen
- företagsportalappen i Android.

#### <a name="support-for-smime-signing-and-encryption-certificates-with-outlook-on-android-fully-managed--5896415-----"></a>Stöd för S/MIME-signering och krypteringscertifikat med Outlook på helt hanterade Android-enheter<!--5896415   -->
Nu kan du använda certifikat för S/MIME-signering och kryptering med Outlook på enheter som kör Android Enterprise Fully Managed.

Det här utökar stödet som lades till förra månaden för andra Android-versioner (stödet för S/MIME-signering och krypteringscertifikat med Outlook i Android). Du kan etablera de här certifikaten med hjälp av importerade SCEP- och PKCS-certifikatprofiler.

Mer information om det här stödet finns i [Känslighetsetiketter och skydd i Outlook för iOS och Android](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/sensitive-labeling-and-protection-outlook-for-ios-android) i Exchange-dokumentationen.

#### <a name="add-a-link-to-your-company-portal-support-website-to-emails-for-noncompliance---7225498------"></a>Lägg till en länk till din företagsportals supportwebbplats dit e-postmeddelanden om inkompatibilitet kan skickas<!-- 7225498    -->
När du [konfigurerar en mall för aviseringsmeddelanden](../protect/actions-for-noncompliance.md#create-a-notification-message-template) för att skicka e-postaviseringar om regelefterlevnad kan du använda den nya inställningen **Länk till företagsportalens webbplats** om du automatiskt vill ta med en länk till företagsportalwebbplatsen. När alternativet har värdet *Aktiverad* kan användare vars enheter inte uppfyller regelefterlevnadskraven och som får ett e-postmeddelande baserat på den här mallen klicka på länken för att komma till en webbplats med mer information om regelöverträdelsen. 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="licensing"></a>Licensiering

#### <a name="admins-no-longer-require-an-intune-license-to-access-microsoft-endpoint-manager-admin-console--1335430---"></a>Administratörer behöver inte längre någon Intune-licens för att komma åt administratörskonsolen för Microsoft Endpoint Manager<!--1335430 -->
Nu kan du ställa in ett reglage för hela klientorganisationen som tar bort kravet på en Intune-licens för att komma åt MEM-administrationskonsolen och API:erna för frågediagram. När du tar bort licenskravet kan du aldrig återställa det igen. 



<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="scripts"></a>Skript 

#### <a name="availability-of-shell-scripts-on-macos-devices---7134839----"></a>Tillgänglighet för shell-skript på macOS-enheter<!-- 7134839  -->
Shell-skript för macOS-enheter är nu tillgängliga i myndighetsmoln och för kinesiska kunder. Mer information om shell-skript finns i [Använda shell-skript på macOS-enheter i Intune](../apps/macos-shell-scripts.md).



<!-- ########################## -->
## <a name="week-of-june-8-2020"></a>Veckan som inleds med 8 juni 2020   

### <a name="app-management"></a>Apphantering  

#### <a name="updates-to-informational-screen-in-company-portal-for-iosipados---7032452---"></a>Uppdatering av informationsskärmen i företagsportalen för iOS/iPad <!--7032452 -->
En informationsskärm i företagsportalen för iOS/iPad har uppdaterats med en bättre förklaring av vad administratörer kan se och göra på enheter. Förtydligandena gäller bara företagsägda enheter. Det är bara texten som har uppdaterats, det har inte gjorts några faktiska ändringar av vad administratörer kan se och göra på användarenheter. Om du vill se de uppdaterade skärmarna går du till [Uppdateringar i användargränssnittet för Intunes slutanvändarappar](./whats-new-app-ui.md).

#### <a name="updated-android-app-conditional-launch-end-user-experience---5736084---"></a>Uppdaterad slutanvändarupplevelse för villkorsstyrd start av Android APP<!-- 5736084 -->
2006-versionen av Android Företagsportal har ändringar som bygger på uppdateringarna från 2005-versionen. 2005 lanserade vi en uppdatering där slutanvändare av Android-enheter som får en varning, blockering eller rensning via en appskyddspolicy ser en helsida som beskriver orsaken till varningen, blockeringen eller rensningen och stegen för att åtgärda problemet. 2006 leds förstagångsanvändare i Android-appar som får en appskyddspolicy tilldelad genom ett guidat flöde för att åtgärda problem som orsakar att deras appåtkomst blockeras. 

<!-- ########################## -->
## <a name="week-of-may-25-2020"></a>Den vecka som börjar 25 maj 2020

### <a name="app-management"></a>Apphantering

#### <a name="windows-32-bit-x86-apps-on-arm64-devices---5477661---"></a>Windows 32-bitars (x86) appar på ARM64-enheter<!-- 5477661 -->
Windows 32-bitars (x86) appar som distribueras som tillgängliga för ARM64-enheter visas nu i Företagsportalen. Mer information om Windows 32-bitars appar finns i [Win32-apphantering](../apps/apps-win32-app-management.md).

#### <a name="windows-company-portal-app-icon---7114635---"></a>Ikon för Windows-företagsportalapp<!-- 7114635 -->
Ikonen för Windows företagsportalappen har uppdaterats. Mer information om företagsportalen finns i [Anpassa Intune-företagsportalappar, företagsportalens webbplats och Intune-appen](../apps/company-portal-app.md).


<!-- ########################## -->
## <a name="week-of-may-18-2020"></a>Den vecka som börjar 18 maj 2020

### <a name="app-management"></a>Apphantering  

#### <a name="update-to-icons-in-company-portal-app-for-iosipados-and-macos--6057697---"></a>Uppdatera till ikoner i företagsportalappen för iOS/iPadOS och macOS<!--6057697 -->
Vi har uppdaterat ikonerna i Företagsportalen för att skapa ett modernt utseende och känsla som stöds på enheter med dubbla skärmar och som är kompatibla med Microsoft Fluent-designsystemet. Om du vill se de uppdaterade ikonerna, går du till [UI-uppdateringar för Intune-slutanvändarappar](./whats-new-app-ui.md). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Enhetssäkerhet

#### <a name="use-endpoint-detection-and-response-policy-to-onboard-devices-to-defender-atp---7130165----"></a>Använd policyn Slutpunktsidentifiering och svar till att registrera enheter i Defender ATP<!-- 7130165  -->

Använd Endpoint Security-policyn [Slutpunktsidentifiering och svar](../protect/endpoint-security-edr-policy.md) (EDR) till att registrera och konfigurera enheter i distributionen av Microsoft Defender Advanced Threat Protection (Defender ATP). EDR har stöd för policyer för Windows-enheter som hanteras via Intune (MDM) och en separat policy för Windows-enheter som hanteras via Configuration Manager. 

Om du vill använda policyn för Configuration Manager-enheter måste du [konfigurera Configuration Manager med stödet för EDR-policyn](../protect/tenant-attach-intune.md). I konfigurationen måste du bland annat:

- Konfigurera Configuration Manager for *anslutning av klientorganisationen*.
- Installera en konsoluppdatering för Configuration Manager som aktiverar stödet för EDR-policyer. Den här uppdateringen gäller endast för hierarkier som har aktiverat *anslutning av klientorganisationer*.
- Synkronisera dina enhetssamlingar från hierarkin till administrationscentret för Microsoft Endpoint Manager.


<!-- ########################## -->
## <a name="week-of-may-11-2020-2005-service-release"></a>Veckan som börjar den 11 maj 2020 (2005 Service Release)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Apphantering

#### <a name="customize-self-service-device-actions-in-the-company-portal--4393379---"></a>Anpassa åtgärder för självbetjäningsenhet i Företagsportal<!--4393379 -->
Du kan anpassa vilka självbetjäningsåtgärder som visas för slutanvändare i appen Företagsportal och på webbplatsen. För att förhindra oavsiktliga enhetsåtgärder kan du konfigurera de här inställningarna för appen Företagsportal genom att välja **Administration av klientorganisation** > **Anpassning**. Följande alternativ är tillgängliga:
- Dölj knappen **Ta bort** på Windows-företagsenheter.
- Dölj knappen **Återställ** på Windows-företagsenheter.
- Dölj knappen **Återställ** på iOS-företagsenheter.
- Dölj knappen **Ta bort** på iOS-företagsenheter.
Mer information finns i [Åtgärder för självbetjäningsenhet för användare från företagsportalen](../apps/company-portal-app.md#user-self-service-device-actions-from-the-company-portal).

#### <a name="auto-update-vpp-available-apps---3640511----"></a>Uppdatera VPP-tillgängliga appar automatiskt<!-- 3640511  -->
Appar som är publicerade som VPP-tillgängliga appar (VPP) uppdateras automatiskt när **Automatisk uppdatering av appar** är aktiverat för VPP-token. Tidigare uppdaterades inte VPP-tillgängliga appar automatiskt. Slutanvändarna behövde i stället gå till Företagsportal och installera om appen om det fanns en nyare version. Obligatoriska appar har fortfarande stöd för automatiska uppdateringar.




#### <a name="android-company-portal-user-experience---5736084----"></a>Användarupplevelsen i företagsportalen för Android<!-- 5736084  -->
I 2005-versionen av Android Företagsportal kommer slutanvändare på Android-enheter som får en varning, blockering eller rensning via en appskyddspolicy att se en ny användarupplevelse. I stället för den nuvarande dialogrutan ser slutanvändarna ett meddelande som beskriver orsaken till varningen, blockeringen eller rensningen och stegen för att åtgärda problemet. Mer information finns i [Appskyddsupplevelse för Android-enheter](../apps/app-protection-policy.md#app-protection-experience-for-android-devices) och [Inställningar för Android-appskyddsprinciper i Microsoft Intune](../apps/app-protection-policy-settings-android.md).

#### <a name="support-for-multiple-accounts-in-company-portal-for-macos---5779449----"></a>Stöd för flera konton i Företagsportal för macOS<!-- 5779449  -->
Företagsportal för macOS-enheter cachelagrar nu användarkonton, vilket gör det enklare att logga in. Användare behöver inte längre logga in i Företagsportal varje gång de startar programmet. Dessutom visar Företagsportal en kontoväljare om flera användarkonton är cachelagrade, så att användarna inte behöver ange sitt användarnamn. 

#### <a name="newly-available-protected-apps---7060934-----"></a>Nyligen tillgängliga skyddade appar<!-- 7060934   -->
Följande skyddade appar är nu tillgängliga:
- Board Papers
- Breezy for Intune
- Hearsay Relate for Intune
- ISEC7 Mobile Exchange Delegate for Intune
- Lexmark for Intune
- Meetio Enterprise
- Microsoft Whiteboard
- Now® Mobile - Intune
- Qlik Sense Mobile 
- ServiceNow® Agent - Intune
- ServiceNow® Onboarding - Intune
- Smartcrypt for Intune
- Tact for Intune
- Zero - email for attorneys

Mer information om skyddade appar finns i [Microsoft Intune-skyddade appar](../apps/apps-supported-intune-apps.md).

#### <a name="search-the-intune-docs-from-the-company-portal---1736480-----"></a>Söka i Intune-dokument från Företagsportal<!-- 1736480   -->
Nu kan du söka i Intune-dokumentationen direkt från appen Företagsportal för macOS. Välj **Hjälp** > **Sök** i menyfältet och ange några nyckelord för att snabbt hitta svar på dina frågor.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Enhetskonfiguration

#### <a name="improvements-to-oemconfig-support-for-zebra-technologies-devices---4184154---"></a>Förbättringar av OEMConfig-stödet för Zebra Technologies-enheter<!-- 4184154 -->
Intune har fullständigt stöd för alla funktioner som tillhandahålls av Zebra OEMConfig. Kunder som hanterar Zebra Technologies-enheter med Android Enterprise och OEMConfig kan distribuera flera OEMConfig-profiler till samma enhet. Kunder kan också visa omfattande rapportering om statusen för sina Zebra OEMConfig-profiler.

Mer information finns i [Distribuera flera OEMConfig-profiler till Zebra-enheter i Microsoft Intune](../configuration/oemconfig-zebra-android-devices.md).

OEMConfig-beteendet ändras inte för andra OEM-tillverkare.

Gäller för:
- Android enterprise
- Zebra Technologies-enheter med stöd för OEMConfig. Om du vill veta mer om support kontaktar du Zebra.

#### <a name="configure-system-extensions-on-macos-devices---6255624---"></a>Konfigurera systemtillägg på macOS-enheter<!-- 6255624 -->
På macOS-enheter kan du skapa en kernel-tilläggsprofil för att konfigurera inställningar på kernelnivå (**Enheter** > **Konfigurationsprofiler** > **macOS** för plattformen > **Kernel-tillägg** för profiler). Apple håller på att återkalla kerneltillägg och ska ersätta dem med systemtillägg i en framtida version.

Systemtillägg körs i användarmiljön och har inte tillgång till kerneln. Målet är att öka säkerheten och ge mer kontroll till slutanvändaren, samtidigt som attacker på kernelnivå begränsas. Med både kerneltillägg och systemtillägg kan användare installera apptillägg som utökar de inbyggda funktionerna i operativsystemet.

I Intune kan du konfigurera både kerneltillägg och systemtillägg (**Enheter** > **Konfigurationsprofiler** > **macOS** för plattformen > **Systemtillägg** för profiler). Kerneltillägg gäller för 10.13.2 och senare. Systemtillägg gäller för 10.15 och senare. Från macOS 10.15 till macOS 10.15.4 kan kerneltillägg och systemtillägg användas tillsammans. 

Information om de här tilläggen för macOS-enheter finns i [Lägga till macOS-tillägg](../configuration/kernel-extensions-overview-macos.md).

Gäller för:
- macOS 10.15 och senare

#### <a name="configure-app-and-process-privacy-preferences-on-macos-devices---2934232-----"></a>Konfigurera sekretessinställningar för appar och processer på macOS-enheter<!-- 2934232   --> 
Med lanseringen av macOS Catalina 10.15 har Apple lagt till nya förbättringar av säkerhet och sekretess. Som standard kan program och processer inte komma åt specifika data utan användarmedgivande. Om användarna inte samtycker kanske inte programmen och processerna fungerar. Intune lägger till stöd för inställningar som gör att IT-administratörer kan tillåta eller neka medgivande för dataåtkomst åt slutanvändare på enheter som kör macOS 10.14 och senare. De här inställningarna ser till att program och processer fortsätter att fungera korrekt och minskar antalet uppmaningar. 

Mer information om de inställningar du kan hantera finns i [Sekretessinställningar i macOS](../configuration/device-restrictions-macos.md#privacy-preferences).

Gäller för:
- macOS 10.14 och senare

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Enhetsregistrering

#### <a name="enrollment-restrictions-support-scope-tags--4209550----"></a>Stöd för omfångstaggar i registreringsbegränsningar<!--4209550  -->
Nu kan du tilldela omfångstaggar i registreringsbegränsningar. Det gör du genom att gå till [Administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Enheter** > **Registreringsbegränsningar** > **Skapa begränsning**. Skapa någon typ av begränsning så visas sidan **Omfångstaggar**. Mer information finns i [Konfigurera registreringsrestriktioner](../enrollment/enrollment-restrictions-set.md).

#### <a name="autopilot-support-for-hololens-2-devices--6305220----"></a>Autopilot-stöd för HoloLens 2-enheter<!--6305220  -->
Windows Autopilot har nu stöd för HoloLens 2-enheter. Mer information om att använda Autopilot för Hololens finns i [Windows Autopilot för HoloLens 2](https://docs.microsoft.com/hololens/hololens2-autopilot).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Enhetshantering

#### <a name="use-sync-remote-action-in-bulk-for-ios--6440956--idmiss--"></a>Använda fjärrsynkronisering som massåtgärd i iOS<!--6440956  idmiss-->
Nu kan du använda åtgärden fjärrsynkronisering för upp till 100 iOS-enheter åt gången. Om du vill se den här funktionen går du till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Enheter** > **Alla enheter** > **Massåtgärder för enheter**. 

#### <a name="automated-device-sync-interval-down-to-12-hours--3077535----"></a>Automatiskt intervall för synkronisering av enheter sänks till 12 timmar<!--3077535  -->
För Apples Automated Device Enrollment har det automatiserade synkroniseringsintervallet mellan Intune och Apple Business Manager sänkts från 24 timmar till 12 timmar. Mer information om synkronisering finns i [Synkronisering av hanterade enheter](../enrollment/device-enrollment-program-enroll-ios.md#sync-managed-devices).


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Enhetssäkerhet

#### <a name="derived-credentials-support-for-disa-purebred-on-android-devices---6939073-------"></a>Stöd för härledda autentiseringsuppgifter för DISA Purebred på Android-enheter<!-- 6939073     -->
Nu kan du använda *DISA Purebred* som provider för [härledda autentiseringsuppgifter](../protect/derived-credentials.md) på helt hanterade Android Enterprise-enheter. I stödet ingår att du kan hämta en härledd autentiseringsuppgift för DISA Purebred. Du kan använda en härledd autentiseringsuppgift till appautentisering, Wi-Fi, VPN eller S/MIME-signering och/eller kryptering med appar som har stöd för det. 

#### <a name="send-push-notifications-as-an-action-for-noncompliance----1733150-----"></a>Skicka push-meddelanden som en åtgärd när efterlevnadsreglerna inte uppfylls <!-- 1733150   -->
Nu kan du konfigurera en [åtgärd när efterlevnadsreglerna inte uppfylls](../protect/actions-for-noncompliance.md#available-actions-for-noncompliance) som skickar ett push-meddelande till användaren om enheten inte uppfyller ett av villkoren i en efterlevnadspolicy. Den nya åtgärden är **Skicka push-meddelande till slutanvändaren** kan användas på Android- och iOS-enheter.

När användarna väljer push-meddelandet på enheten öppnas Företagsportal- eller Intune-appen med information om vilken regel som inte uppfylls.

#### <a name="endpoint-security-content-and-new-features---5720009-5892558-7130145-5653324-7140602----"></a>Endpoint Security-innehåll och nya funktioner<!-- 5720009 5892558, 7130145, 5653324, 7140602  -->

Nu är dokumentationen för [Endpoint Security](../protect/endpoint-security.md) tillgänglig. I noden Endpoint Security i administrationscentret för Microsoft Endpoint Manager kan du nu:

- Skapa och distribuera fokuserade säkerhetspolicyer till dina hanterade enheter
- Konfigurera integrering med Microsoft Defender Advanced Threat Protection och hantera säkerhetsaktiviteter som åtgärdar de enheter utsatta för risk som ATP-teamet identifierar
- Konfigurera säkerhetsbaslinjer
- Hantera policyer för enheters efterlevnad och villkorsstyrd åtkomst
- Visa efterlevnadsstatus för alla enheter från både Intune och Configuration Manager när Configuration Manager är konfigurerat för klientanslutning.

Utöver tillgängligheten för innehåll är det här några nyheter i Endpoint Security den här månaden:

- [**Endpoint Security-policyer**](../protect/endpoint-security-policy.md) **är inte längre i** ***förhandsversion*** och är nu redo att användas i produktionsmiljöer, som *allmänt tillgängliga*, med två undantag:

  - I en ny *offentlig förhandsversion* kan du använda profilen [**Microsoft Defender-brandväggsregler** ](../protect/endpoint-security-firewall-policy.md#firewall-profiles) som brandväggspolicy i Windows 10. Med varje instans av den här profilen kan du konfigurera upp till 150 brandväggsregler som komplement till dina Microsoft Defender-brandväggsprofiler. 
  - Policyn för kontoskydd är fortfarande i förhandsversion. 

- Nu kan du [**kopiera policyer för slutpunktsskydd**](../protect/endpoint-security-policy.md#duplicate-a-policy). Kopiorna behåller samma inställningskonfiguration som den ursprungliga principen, men får ett nytt namn. Den nya policyinstansen innehåller inte några tilldelningar till grupper förrän du redigerar den nya policyinstansen och lägger till dem. Du kan kopiera följande policyer:
  - Antivirus
  - Diskkryptering
  - Brandvägg
  - Slutpunktsidentifiering och svar
  - Minska attackytan
  - Kontoskydd

- Nu kan du [**kopiera en säkerhetsbaslinje**](../protect/security-baselines.md#duplicate-a-security-baseline). Kopian behåller samma inställningskonfiguration som den ursprungliga baslinjen, men får ett nytt namn. Den nya baslinjeinstansen innehåller inga tilldelningar till grupper förrän du redigerar den nya baslinjeinstansen och lägger till dem.

- Det finns en ny rapport för Endpoint Security-policyn Antivirus: [**Defekta slutpunkter i Windows 10**](../protect/endpoint-security-antivirus-policy.md#windows-10-unhealthy-endpoints). Den här rapporten är en ny sida du kan välja när du visar Endpoint Security-policyn Antivirus. Rapporten visar antivirusstatus för dina MDM-hanterade Windows 10-enheter.  

#### <a name="support-for-smime-signing-and-encryption-certificates-with-outlook-on-android---7207474----"></a>Stöd för S/MIME-signering och krypteringscertifikat med Outlook i Android<!-- 7207474  -->
Nu kan du använda certifikat för S/MIME-signering och kryptering med Outlook i Android. Med det här stödet kan du etablera certifikaten med hjälp av SCEP, PKCS och importerade PKCS-certifikatprofiler. Följande Android-plattformar stöds:

- Android Enterprise-arbetsprofil
- Android-enhetsadministratör

Stödet för helt hanterade Android Enterprise-enheter kommer snart.

Mer information om det här stödet finns i [Känslighetsetiketter och skydd i Outlook för iOS och Android](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/sensitive-labeling-and-protection-outlook-for-ios-android) i Exchange-dokumentationen.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Övervaka och felsöka

#### <a name="device-reports-ui-update---6269408---"></a>Uppdatering av gränssnittet för enhetsrapporter<!-- 6269408 -->
I rapportöversikten finns nu flikarna **Sammanfattning** och **Rapporter**. I [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) väljer du **Rapporter** och sedan fliken **Rapporter** för att se de tillgängliga rapporttyperna. Mer information finns i [Intune-rapporter](../fundamentals/reports.md).


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="scripting"></a>Använda skript

#### <a name="macos-script-support---6376978----"></a>stöd för macOS-skript<!-- 6376978  -->
Nu är skriptstöd för macOS allmänt tillgängligt. Dessutom har vi lagt till stöd för både användartilldelade skript och macOS-enheter som har registrerats med Apples Automated Device Enrollment (tidigare Programmet för enhetsregistrering). Mer information finns i [Använda Shell-skript på macOS-enheter i Intune](../apps/macos-shell-scripts.md).


<!-- ########################## -->
## <a name="week-of-may-4-2020"></a>Den vecka som börjar 4 maj 2020  

### <a name="company-portal-for-android-guides-users-to-get-apps-after-work-profile-enrollment----6103999---"></a>Företagsportal för Android hjälper användarna att hämta appar utifrån registreringen av arbetsprofilen <!-- 6103999 -->
Vi förbättrar vägledningen i appen i Företagsportal så att användarna enklare kan hitta och installera appar. När användaren har registrerat sin arbetsprofil ser de ett meddelande som förklarar att de kan hitta föreslagna appar i den märkta versionen av Google Play. Det sista steget i [Registrera enhet med Android-profil](../user-help/enroll-device-android-work-profile.md) har uppdaterats för att visa det nya meddelandet. Användarna ser också den nya länken **Hämta appar** i Företagsportal-lådan till vänster. För att möjliggöra det här har vi tagit bort fliken **APPAR**. Om du vill se de uppdaterade skärmarna går du till [Uppdateringar i användargränssnittet för Intunes slutanvändarappar](./whats-new-app-ui.md). 

<!-- ########################## -->
## <a name="week-of-april-20-2020"></a>Veckan som börjar 20 april 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Enhetshantering

#### <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions---6317104-cm3555758----"></a>Ansluta Microsoft Endpoint Manager-klientorganisation: Enhetssynkronisering och enhetsåtgärder<!-- 6317104, CM3555758  -->
Microsoft Endpoint Manager sammanfogar Configuration Manager och Intune i en enda konsol. Från och med Configuration Manager version 2002 kan du ladda upp dina Configuration Manager-enheter till molntjänsten och vidta åtgärder i administrationscentret. Mer information finns i [Microsoft Endpoint Manager-klientorganisation: Enhetssynkronisering och enhetsåtgärder](../../configmgr/tenant-attach/device-sync-actions.md). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Apphantering

#### <a name="microsoft-office-365-proplus-rename---6368143---"></a>Nytt namn för Microsoft Office 365 ProPlus<!-- 6368143 -->
Microsoft Office 365 ProPlus har bytt namn till **Microsoft 365 Apps for enterprise**. Läs mer i [Nytt namn för Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). I vår dokumentation kallar vi det ofta för Microsoft 365 Apps. I [administrationscenter för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) hittar du Apps-serien genom att välja **Apps** > **Windows** > **Lägg till**. Mer information om hur du lägger till appar finns i [Lägga till appar i Microsoft Intune](../apps/apps-add.md).

<!-- ########################## -->
## <a name="week-of-april-13-2020-2004-service-release"></a>Veckan för den 13 april 2020 (2004 tjänstversion)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Apphantering

#### <a name="manage-smime-settings-for-outlook-on-android-enterprise-devices---6517085-----"></a>Hantera S/MIME-inställningar för Outlook på Android Enterprise-enheter<!-- 6517085   -->
Du kan använda appkonfigurationsprinciper för att hantera S/MIME-inställningen för Outlook på enheter som kör Android Enterprise. Du kan också välja om enhetsanvändare ska kunna aktivera eller inaktivera S/MIME i Outlook-inställningarna eller inte. Om du vill använda appkonfigurationsprinciper för Android går du till [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) och väljer **Appar** > **Appkonfigurationsprinciper** > **Lägg till** > **Hanterade enheter**. Mer information om hur du konfigurerar inställningar för Outlook finns i [konfigurationsinställningar för Microsoft Outlook](../apps/app-configuration-policies-outlook.md).

#### <a name="pre-release-testing-for-managed-google-play-apps---2681933----"></a>Förhandstestning för hanterade Google Play-appar<!-- 2681933  -->
Organisationer som använder [Google Plays slutna testkanaler för förhandstestning av appar](https://support.google.com/googleplay/android-developer/answer/3131213) kan hantera dessa kanaler med Intune. Du kan selektivt tilldela appar (som publiceras på Google Plays förproduktionskanaler) till pilotgrupper för testning. I Intune kan du se om en app har en testkanal med en publicerad förproduktionsversion, och du kommer att kunna tilldela den kanalen till grupper med Azure AD-användare eller -enheter. Den här funktionen är tillgänglig för alla våra aktuella Android Enterprise-scenarier (arbetsprofil, fullständigt hanterad, särskilt avsedd). I [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) kan du lägga till en hanterad Google Play-app genom att välja **Appar** > **Android** > **Lägg till**. Mer information finns i [Working with Managed Google Play Closed Testing Tracks](../apps/apps-add-android-for-work.md#working-with-managed-google-play-closed-testing-tracks) (arbeta med testspår på Hanterat Google Play-konto).

#### <a name="microsoft-teams-is-now-included-in-the-office-365-suite-for-macos---5903936----"></a>Microsoft Teams ingår nu i Office 365-paketet för macOS<!-- 5903936  -->
Användare som tilldelas Microsoft Office för macOS i Microsoft Endpoint Manager får förutom de vanliga Microsoft Office-apparna (Word, Excel, PowerPoint, Outlook och OneNote) nu även Microsoft Teams. Intune identifierar befintliga Mac-enheter som har andra Office för macOS-appar installerade och kommer att försöka installera Microsoft Teams nästa gång enheten checkar in med Intune. I [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) kan du hitta **Office 365-paketet** för macOS genom att välja **Appar** > **macOS** > **Lägg till**. Mer information finns i [Tilldela Office 365 till macOS-enheter med Microsoft Intune](../apps/apps-add-office365-macos.md).

#### <a name="update-to-android-app-configuration-policies---6113334----"></a>Uppdatering av konfigurationsprinciper för Android-appar<!-- 6113334  -->
Konfigurationsprinciperna för Android-appar har uppdaterats så att administratörer kan välja typ av enhetsregistrering innan de skapar konfigurationsprofiler för appar. Funktionen läggs till i kontot för certifikatprofiler som baseras på registreringstyp (arbetsprofil eller enhetsägare).  Den här uppdateringen innehåller följande:

1. Om en ny profil skapas och arbetsprofil och enhetsägarprofil väljs som enhetsregistreringstyp kan du inte associera en certifikatprofil med appkonfigurationsprincipen.
2. Om en ny profil skapas och Endast arbetsprofil har valts kan de certifikatprinciper för arbetsprofil som skapats under Enhetskonfiguration användas.
3. Om en ny profil skapas och Endast enhetens ägare har valts kan de certifikatprinciper för enhetsägare som skapats under Enhetskonfiguration användas. 

> [!IMPORTANT]
> För de befintliga principer som skapats före lanseringen av den här funktionen (april 2020, version 2004) och som inte har några associerade certifikatprofiler, används som standard arbetsprofil och enhetsägarprofil som enhetsregistreringstyp. Även för de befintliga principer som skapats före lanseringen av den här funktionen och som har associerade certifikatprofiler, används som standard endast arbetsprofil.

Vi lägger också till e-postkonfigurationsprofiler för Gmail och Nine som fungerar för både registreringstypen Arbetsprofil och Enhetsägare. Detta innefattar användning av certifikatprofiler på båda e-postkonfigurationstyperna.  Alla Gmail- eller Nine-principer som du har skapat under Enhetskonfiguration för arbetsprofiler fortsätter att gälla för enheten och du behöver inte flytta dem till appkonfigurationsprinciper.

I [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) hittar du appkonfigurationsprinciperna genom att välja **Appar** > **Appkonfigurationsprinciper**. Mer information om appkonfigurationsprinciper finns i [Appkonfigurationsprinciper för Microsoft Intune](../apps/app-configuration-policies-overview.md).

#### <a name="push-notification-when-device-ownership-type-is-changed---5575875---"></a>Push-meddelande när ägarskapstypen för enheten ändras<!-- 5575875 -->
Du kan konfigurera ett push-meddelande till användarna av företagsportalsappen (både Android och iOS) när deras ägarskapstyp ändras från Personlig till Företag som en integritetsmeddelande. Push-meddelandet är inställt på av som standard. Inställningen hittar du i Microsoft Endpoint Manager genom att välja **Innehavaradministration** > **Anpassning**. Mer information om hur enhetsägarskapet påverkar slutanvändarna finns i [Ändra enhetsägande](../enrollment/corporate-identifiers-add.md#change-device-ownership).

#### <a name="group-targeting-support-for-customization-pane---4722837----"></a>Stöd för riktning till grupper i fönstret Anpassning<!-- 4722837  -->
Du kan rikta inställningarna i fönstret **Anpassning** till användargrupper. Du hittar de här inställningarna i Intune genom att gå till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), välja **Administration av klientorganisation** > **Anpassning**. Mer information om anpassning finns i [Anpassa Intune-företagsportalens appar, företagsportalens webbplats och Intune-appen](../apps/company-portal-app.md).


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Enhetskonfiguration

#### <a name="multiple-evaluate-each-connection-attempt-on-demand-vpn-rules-supported-on-ios-ipados-and-macos---6424615----"></a>Flera VPN-regler på begäran för att utvärdera varje anslutningsförsök som stöds på iOS, iPad och macOS<!-- 6424615  -->
Användarupplevelsen i Intune tillåter flera VPN-regler på begäran i samma VPN-profil med åtgärden **Utvärdera varje anslutningsförsök** (**enheter** > **Konfigurationsprofiler** > **Skapa profil** > **iOS/iPad** eller **macOS** för plattform > **VPN** för profilen > **Automatisk VPN** > **På begäran**).

Den använde enbart den första regeln i listan. Det här beteendet har åtgärdats, och Intune utvärderar alla regler i listan. Varje regel utvärderas i den ordning som den visas i listan över regler på begäran.

> [!NOTE]
> Om du har befintliga VPN-profiler som använder dessa VPN-regler på begäran tillämpas åtgärden nästa gång du ändrar VPN-profilen. Du kan till exempel göra en mindre ändring, t. ex. ändra anslutningens namn, och sedan spara profilen.
>
> Om du använder SCEP-certifikat för autentisering orsakar den här ändringen att certifikaten för VPN-profilen utfärdas igen.

Gäller för:
- iOS/iPadOS
- macOS

Mer information om VPN-profiler finns i [Skapa VPN-profiler](../configuration/vpn-settings-configure.md).

#### <a name="additional-options-in-sso-and-sso-app-extension-profiles-on-iosipados-devices---6504155-----"></a>Ytterligare alternativ i SSO- och SSO-apptilläggsprofiler på iOS/iPadOS-enheter<!-- 6504155   -->

På iOS/iPadOS-enheter kan du:
- Ange SAM-kontonamnet (Hanteraren för kontosäkerhet) som Kerberos-huvudnamn i SSO-profiler (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **iOS/iPadOS** som plattform > **Enhetsfunktioner** som profil > **Enkel inloggning**). 
- Konfigurera Microsoft Azure AD-tillägget för iOS/iPadOS med färre klick med hjälp av den nya SSO-apptilläggstypen i SSO-apptilläggsprofiler (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **iOS/iPadOS** som plattform > **Enhetsfunktioner** som profil > **Tillägg för enkel inloggning**). Du kan aktivera Azure AD-tillägget för enheter i läget för delade enheter och skicka tilläggsspecifika data till tillägget.

Gäller för:
- iOS/iPadOS 13.0+

Mer information om hur du använder enkel inloggning på iOS/iPadOS-enheter finns i [Tilläggsöversikten för enkel inloggning](../configuration/device-features-configure.md#single-sign-on-app-extension) och [listan med inställningar för enkel inloggning](../configuration/ios-device-features-settings.md#single-sign-on-app-extension).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Enhetsregistrering

#### <a name="delete-apple-automated-device-enrollment-token-when-default-profile-is-present--6393220---"></a>Ta bort Apples token för automatisk enhetsregistrering när standardprofilen finns<!--6393220 -->
Tidigare gick det inte att ta bort en standardprofil, vilket innebar att du inte kunde ta bort det token för automatisk enhetsregistrering som var associerat med profilen. Nu kan du ta bort ett token när:
- inga enheter har tilldelats till token
- det finns en standardprofil för detta. Ta bort standardprofilen och ta sedan bort associerat token.
Mer information finns i [Ta bort en ADE-token från Intune](../enrollment/device-enrollment-program-enroll-ios.md#delete-an-automated-device-enrollment-token-from-intune).

#### <a name="scaled-up-support-for-apple-automated-device-enrollment-and-apple-configurator-2-devices-profiles-and-tokens--3542402---"></a>Skalbart stöd för Apples automatiserade enhetsregistrering och Apple Configurator 2-enheter, profiler och token<!--3542402 -->
För att hjälpa distribuerade IT-avdelningar och organisationer stöder Intune nu upp till 1 000 registreringsprofiler per token, 2 000 token för automatiserad enhetsregistrering (kallades tidigare DEP) per Intune-konto, och 75 000 enheter per token. Det finns ingen specifik gräns för enheter per registreringsprofil under det högsta antalet enheter per token.

Intune stöder nu upp till 1 000 Apple Configurator 2-profiler.

Mer information finns i [Volym som stöds](../enrollment/device-enrollment-program-enroll-ios.md#supported-volume).

#### <a name="all-devices-page-column-entry-changes--6967616---"></a>Ändrade kolumnposter på sidan Alla enheter<!--6967616 -->
På sidan **Alla enheter** har posterna för kolumnen **Hanterad av** ändrats:
- *Intune* visas nu i stället för *MDM*
- *Samhanterade* visas nu i stället för *MDM/ConfigMgr-agenten*

Exportvärdena är oförändrade.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Enhetshantering

#### <a name="trusted-platform-manager-tpm-version-information-now-on-device-hardware-page--6224914-idmiss---"></a>Versionsinformation för Trusted Platform Manager (TPM) nu på enhetens maskinvarusida<!--6224914 idmiss -->
Nu kan du se TPM-versionsnumret på enhetens maskinvarusida ([administrationscenter för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Enheter** > välja en enhet > **Maskinvara** > titta under **Systemomslutning**).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Övervaka och felsöka

#### <a name="collect-logs-to-better-troubleshoot-scripts-assigned-to-macos-devices---6359853----"></a>Samla in loggar för bättre felsökning av skript som är tilldelade till macOS-enheter<!-- 6359853  -->
Du kan nu samla in loggar för bättre felsökning av skript som har tilldelats macOS-enheter. Du kan samla in loggar upp till 60 MB (komprimerade) eller 25 filer, beroende på vilket som inträffar först. Mer information finns i [Troubleshoot macOS shell script policies using log collection](../apps/macos-shell-scripts.md#troubleshoot-macos-shell-script-policies-using-log-collection) (felsöka principer för macOS-kommandoskript med logginsamling).
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="security"></a>Säkerhet

#### <a name="derived-credentials-to-provision-android-enterprise-fully-managed-devices-with-certificates--4839592------"></a>Härledda autentiseringsuppgifter för att etablera fullständigt hanterade Android Enterprise-enheter med certifikat<!--4839592    -->
Intune stöder nu användning av [härledda autentiseringsuppgifter](../protect/derived-credentials.md) som autentiseringsmetod för Android-enheter. Härledda autentiseringsuppgifter är en implementering av National Institute of Standards and Technology (NIST) 800-157-standarden för distribution av certifikat till enheter. Vårt stöd för Android är en utveckling av vårt stöd för enheter som kör iOS/iPad.

Härledda autentiseringsuppgifter är beroende av att ett PIV-kort (Personal Identity Verification) eller ett CAC-kort (Common Access Card) används, till exempel ett smartkort. För att få en härledd autentiseringsuppgift för sin mobila enhet börjar användare i Microsoft Intune-appen och följer ett registreringsarbetsflöde som är unikt för den provider som du använder. Gemensamt för alla providrar är kravet på användning av ett smartkort på en dator för autentisering till providern för den härledda autentiseringsuppgiften. Providern utfärdar sedan ett certifikat till den enhet som härleds från användarens smartkort.

Du kan använda härledda autentiseringsuppgifter som autentiseringsmetod för enhetskonfigurationsprofiler för VPN och Wi-Fi. Du kan även använda dem för appautentisering samt för S/MIME-signering och -kryptering för program som har stöd för det.

Intune stöder nu följande leverantörer för härledda autentiseringsuppgifter med Android:
- Entrust Datacard
- Intercede

En tredje leverantör, DISA Purebred, blir tillgänglig för Android i en framtida version.

#### <a name="microsoft-edge-security-baseline-is-now-generally-available--6586139---"></a>Microsoft Edge säkerhetsbaslinje är nu allmänt tillgängligt<!--6586139 -->

En ny version av [Microsoft Edge säkerhetsbaslinje](../protect/security-baselines.md#available-security-baselines) är nu tillgänglig och släpps som allmänt tillgänglig (GA). Den tidigare Edge-baslinjen fanns som förhandsversion.  Den nya baslinjeversionen är april 2020 (Microsoft Edge version 80 och senare). 

I och med lanseringen av den nya baslinjen kan du inte längre skapa profiler baserade på tidigare baslinjeversioner, men du kan fortsätta att använda profiler som du har skapat med dessa versioner. Du kan också välja att [uppdatera dina befintliga profiler så att de använder den senaste baslinjeversionen](../protect/security-baselines.md#change-the-baseline-version-for-a-profile). 

<!-- ########################## -->
## <a name="week-of-april-6-2020"></a>Veckan som börjar 6 april 2020

#### <a name="new-shell-script-settings-for-macos-devices---6884363---"></a>Nya Shell-skript-inställningar för macOS-enheter<!-- 6884363 -->
När du konfigurerar Shell-skript för macOS-enheter, kan du nu konfigurera följande nya inställningar: 
- Dölja skriptmeddelanden på enheter
- Skriptfrekvens
- Maximalt antal nya försök om skriptet misslyckas

Mer information finns i [Använda Shell-skript på macOS-enheter i Intune](../apps/macos-shell-scripts.md).

<!-- ########################## -->
## <a name="week-of-march-30-2020"></a>Den vecka som börjar 30 mars 2020

### <a name="new-url-for-the-microsoft-endpoint-manager-admin-center---3704810---"></a>Ny URL för administrationscentret för Microsoft Endpoint Manager<!-- 3704810 -->
För att anpassa efter tillkännagivandet om Microsoft Endpoint Manager på Ignite förra året har vi ändrat URL:en för administrationscentret för Microsoft Endpoint Manager (tidigare Microsoft 365-enhetshantering) till [https://endpoint.microsoft.com](https://endpoint.microsoft.com). Den gamla URL:en för administrationscentret ([https://devicemanagement.microsoft.com](https://devicemanagement.microsoft.com)) fortsätter att fungera, men vi rekommenderar att du börjar använda den nya URL:en för administrationscentret för Microsoft Endpoint Manager.

Mer information finns i [Förenkla IT-uppgifter med hjälp av administrationscentret för Microsoft Endpoint Manager](what-is-device-management.md#simplify-it-tasks-using-the-device-management-admin-center).  


### <a name="app-management"></a>Apphantering  

#### <a name="company-portal-for-ios-supports-landscape-mode--6048329----"></a>Företagsportalen för iOS stödjer liggande läge<!--6048329  -->   
Användare kan nu registrera sina enheter, hitta appar och få IT-support med hjälp av valfri skärmorientering. Appen identifieras automatiskt och anpassar skärmen till stående eller liggande läge, såvida inte användaren låser skärmen i stående läge.  

#### <a name="script-support-for-macos-devices-public-preview---4280361----"></a>Skriptstöd för macOS-enheter (offentlig förhandsversion)<!-- 4280361  -->
Du kan lägga till och distribuera skript till macOS-enheter. Det här stödet utökar din möjlighet att konfigurera macOS-enheter utöver vad som är möjligt med hjälp av interna MDM-funktioner på macOS-enheter. Mer information finns i [Använda Shell-skript på macOS-enheter i Intune](../apps/macos-shell-scripts.md).

<!-- ########################## -->
## <a name="week-of-march-24-2020"></a>Den vecka som börjar 24 mars 2020

### <a name="improved-user-interface-experience-when-creating-device-restrictions-profiles-on-android-and-android-enterprise-devices---5841361---"></a>Förbättrat användargränssnitt när vid skapande av enhetskonfigurationsprofiler på enheter med Android eller Android Enterprise<!-- 5841361 -->
När du skapar en profil för enheter med Android eller Android Enterprise kommer upplevelsen i administrationscentret för slutpunktshantering att uppdateras. Den här ändringen påverkar följande enhetskonfigurationsprofiler (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **Android-enhetsadministratör** eller **Android Enterprise** för plattformen):

- Enhetsbegränsningar: Android-enhetsadministratör
- Enhetsbegränsningar: Android Enterprise-enhetsägare
- Enhetsbegränsningar: Android Enterprise-arbetsprofil

Mer information om enhetsbegränsningar som du kan konfigurera finns i [Android-enhetsadministratör](../configuration/device-restrictions-android.md) och [Android Enterprise](../configuration/device-restrictions-android-for-work.md).

### <a name="improved-user-interface-experience-when-creating-configuration-profiles-on-iosipados-and-macos-devices---5569002-5568997---"></a>Förbättrat användargränssnitt när du skapar konfigurationsprofiler på iOS/iPadOS- och macOS-enheter<!-- 5569002 5568997 -->
När du skapar en profil för iOS- eller macOS-enheter uppdateras funktionen i administrationscentret för slutpunktshantering. Den här ändringen påverkar följande enhetskonfigurationsprofiler (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **iOS/iPadOS** eller **macOS** för plattformen):

- Anpassad: iOS/iPadOS, macOS
- Enhetsfunktioner: iOS/iPadOS, macOS
- Enhetsbegränsningar: iOS/iPadOS, macOS
- Slutpunktsskydd: macOS
- Tillägg: macOS
- Inställningsfil: macOS

### <a name="hide-from-user-configuration-setting-in-device-features-on-macos-devices---6524869---"></a>Dölj från inställningen för användarkonfiguration i enhetsfunktionerna på macOS-enheter<!-- 6524869 -->

När du skapar en konfigurationsprofil för enhetsfunktioner på macOS-enheter finns nu den nya inställningen **Dölj från användarkonfiguration** (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **macOS** för plattformen > **Enhetsfunktioner** för profilen > **Inloggningsalternativ**).

Den här funktionen anger appens markering för dölj i listan **Användare och grupper** för inloggningsalternativ för appen på macOS-enheter. Befintliga profiler visar den här inställningen i listan som inte konfigurerad. Administratörer kan uppdatera befintliga profiler för att konfigurera den här inställningen.

När inställningen är **Dölj** markeras kryssrutan Dölj för appen och användarna kan inte ändra den. Den döljer också appen från användare när användare har loggat in på sina enheter.

> [!div class="mx-imgBorder"]
> ![Dölj appar på macOS-enheter när användare loggar in på enheten i Microsoft Intune och Endpoint Manager](./media/whats-new/macos-hide-checkmark-users-groups-login-items-apps-list.png)

Mer information om de inställningar som du kan konfigurera finns i [Funktionsinställningar för macOS-enheter](../configuration/macos-device-features-settings.md).

Den här funktionen gäller för:

- macOS

<!-- ########################## -->
## <a name="week-of-march-16-2020-2003-service-release"></a>Veckan den 16 mars 2020 (2003 Service Release)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Apphantering

#### <a name="macos-and-ios-company-portal-updates---5779439-5780234----"></a>Uppdateringar av företagsportalen för macOS och iOS<!-- 5779439, 5780234  -->
Profilfönstret i företagsportalen för macOS och iOS har uppdaterats så att det inkluderar utloggningsknappen. Förbättringar av användargränssnittet har gjorts i profilfönstret i macOS-företagsportalen. Mer information om företagsportalen finns i [Så här konfigurerar du Microsoft Intune-företagsportalappen](../apps/company-portal-app.md).

#### <a name="retarget-web-clips-to-microsoft-edge-on-ios-devices---5455276-----"></a>Omdirigera webbklipp till Microsoft Edge på iOS-enheter<!-- 5455276   -->
Nyligen distribuerade webbklipp (fästa webbappar) på iOS-enheter öppnas i Microsoft Edge i stället för Intune Managed Browser om det behövs för att öppna i en skyddad webbläsare. Du måste omdirigera befintliga webbklipp för att se till att de öppnas i Microsoft Edge i stället för Managed Browser. Mer information finns i [Hantera webbåtkomst med hjälp av Microsoft Edge med Microsoft Intune](../apps/manage-microsoft-edge.md) och [Lägg till webbappar i Microsoft Intune](../apps/web-app.md).

#### <a name="use-the-intune-diagnostic-tool-with-microsoft-edge-for-android---4735244----"></a>Använd Intune-diagnostikverktyg med Microsoft Edge för Android<!-- 4735244  -->
Microsoft Edge för Android är nu integrerat med Intune-diagnostikverktyget. På samma sätt som med Microsoft Edge för iOS startar du Intune-diagnostikverktyget genom att ange ”about: intunehelp” i URL-fältet (adressrutan) för Microsoft Edge på enheten. Med det här verktyget får du detaljerade loggar. Användare kan vägledas till att samla in och skicka loggar till IT-avdelningen eller visa MAM-loggar för särskilda appar.

#### <a name="updates-to-intune-branding-and-customization---5236032----"></a>Uppdateringar av Intune-varumärkesanpassning och anpassning<!-- 5236032  -->
Vi har uppdaterat det Intune-fönster som hette ”Varumärkesanpassning och anpassning” med förbättringar såsom följande:

- Byter namn på fönstret till **Anpassning**.
- Förbättrar organiseringen och utformningen av inställningar.
- Förbättrar text och knappbeskrivningar för inställningar.

Du hittar de här inställningarna i Intune genom att gå till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), välja **Administration av klientorganisation** > **Anpassning**. Information om befintlig anpassning finns i [Så här konfigurerar du Microsoft Intune-företagsportalappen](../apps/company-portal-app.md).

#### <a name="users-personal-encrypted-recovery-key---6273943----"></a>Användarens personliga krypterade återställningsnyckel<!-- 6273943  -->
En ny Intune-funktion är tillgänglig som gör att användare kan hämta sin personliga krypterade **FileVault**-återställningsnyckel för Mac-enheter via Android-företagsportalappen eller via Android Intune-programmet. Det finns en länk i både företagsportalappen och Intune-programmet som öppnar en Chrome-webbläsare till webbföretagsportalen, där användaren kan se den **FileVault**-återställningsnyckel som krävs för åtkomst till Mac-enheterna. Mer information om kryptering finns i [Använda enhetskryptering med Intune](../protect/encrypt-devices.md).

#### <a name="optimized-dedicated-device-enrollment----6114580----"></a>Optimerad registrering av dedikerad enhet <!-- 6114580  -->
Vi optimerar registreringen för dedikerade Android Enterprise-enheter och gör det enklare för SCEP-certifikat som är kopplade till Wi-Fi att gälla för dedikerade enheter som registrerats före den 22 november 2019. För nya registreringar fortsätter Intune-appen att installeras, men slutanvändare kommer inte längre behöva utföra steget **Aktivera Intune-agent** under registreringen. Installationen sker automatiskt i bakgrunden och SCEP-certifikat som är kopplade till Wi-Fi kan distribueras och konfigureras utan åtgärder från slutanvändaren.  

Dessa ändringar kommer att lanseras i faser under mars månad samtidigt som Intune-tjänstens serverdel distribueras. Alla klienter kommer att ha det här nya beteendet i slutet av mars. Relaterad information finns i [Stöd för SCEP-certifikat i Android Enterprise-dedikerade enheter](https://techcommunity.microsoft.com/t5/intune-customer-success/support-for-scep-certificates-in-android-enterprise-dedicated/ba-p/928147).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Enhetskonfiguration

#### <a name="new-user-experience-when-creating-administrative-templates-on-windows-devices--5096036---"></a>Ny användarupplevelse när du skapar administrativa mallar på Windows-enheter<!--5096036 -->
Baserat på kundfeedback och vår förflyttning till den nya Azure-helskärmsupplevelsen har vi byggt om profilupplevelsen för administrativa mallar med en mappvy. Vi har inte gjort några ändringar i några inställningar eller befintliga profiler. Det innebär att befintliga profiler förblir desamma och kan användas i den nya vyn. Du kan fortfarande navigera bland alla inställningsalternativ genom att välja **Alla inställningar** och använda Sök. Trädvyn delas av dator- och användarkonfigurationer. Du hittar Windows-, Office- och Edge-inställningar i deras associerade mappar.  

Gäller för:
- Windows 10 och senare

#### <a name="vpn-profiles-with-ikev2-vpn-connections-can-use-always-on-with-iosipados-devices---1947932-----"></a>VPN-profiler med IKEv2 VPN-anslutningar kan använda Alltid på med iOS/iPadOS-enheter<!-- 1947932   -->
På iOS/iPadOS-enheter kan du skapa en VPN-profil som använder en IKEv2-anslutning (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **iOS/iPadOS** för plattformen > **VPN** för profiltypen). Nu kan du uppdatera och konfigurera Alltid på med IKEv2. När IKEv2 VPN-profiler har konfigurerats ansluter de automatiskt och förblir anslutna (eller återansluter snabbt) till VPN-anslutningen. Den förblir ansluten även när du flyttar mellan nätverk eller startar om enheter.

På iOS/iPadOS är Alltid på för VPN begränsat till IKEv2-profiler.

Om du vill se de IKEv2-inställningar som du kan konfigurera går du till [Lägg till VPN-inställningar på iOS-enheter i Microsoft Intune](../configuration/vpn-settings-ios.md#ikev2-settings).

Gäller för:
- iOS/iPadOS

#### <a name="delete-bundles-and-bundle-arrays-in-oemconfig-device-configuration-profiles-on-android-enterprise-devices---5550355-----"></a>Ta bort paket och paketmatriser i OEMConfig-enhetskonfigurationsprofiler på Android Enterprise-enheter<!-- 5550355   -->
På Android Enterprise-enheter kan du uppdatera OEMConfig-profiler (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **Android Enterprise** för plattformen > **OEMConfig** för profiltypen). Användare kan nu ta bort paket och paketmatriser med hjälp av **Configuration Designer** i Intune.

Mer information om OEMConfig-profiler finns i [Använda och hantera Android Enterprise-enheter med OEMConfig i Microsoft Intune](../configuration/android-oem-configuration-overview.md).

Gäller för:
- Android enterprise

#### <a name="configure-the-iosipados-microsoft-azure-ad-sso-app-extension---5672534-----"></a>Konfigurera Microsoft Azure AD SSO-apptillägget för enkel inloggning för iOS/iPadOS<!-- 5672534   -->
Microsoft Azure AD-teamet skapade en app för omdirigering med enkel inloggning som gör att användare med iOS/iPadOS 13.0+ kan få åtkomst till Microsofts appar och webbplatser med en enda inloggning. Alla appar som tidigare hade en asynkron autentisering med Microsoft Authenticator-appen fortsätter att få SSO med det nya SSO-tillägget. Med Azure AD SSO-tillägget för SSO-appen kan du konfigurera SSO-tillägget med apptillägget av typen enkel inloggning (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **iOS/iPad** för plattform > **Enhetsfunktioner** > för profiltyp **Apptillägg för enkel inloggning**).

Gäller för:
- iOS 13.0 och senare
- iPadOS 13.0 och senare

Mer information om iOS-apptillägg för enkel inloggning finns i [Apptillägg för enkel inloggning](../configuration/device-features-configure.md#single-sign-on-app-extension).

#### <a name="enterprise-app-trust-settings-modification-setting-is-removed-from-iosipados-device-restriction-profiles---6225131-----"></a>Inställningen Ändringar av inställningar för att lita på företagsappar tas bort från profiler för iOS-/iPadOS-enhetsbegränsningar<!-- 6225131   -->
På enheter med iOS/iPadOS skapar du en enhetsbegränsningsprofil (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **iOS/iPadOS** för plattform > **Enhetsbegränsningar** för profiltyp). Inställningen **Ändringar av inställningar för att lita på företagsappar** tas bort av Apple och tas bort från Intune. Om du för närvarande använder den här inställningen i en profil har den ingen effekt och tas bort från befintliga profiler. Den här inställningen tas även bort från all rapportering i Intune.

Gäller för:
- iOS/iPadOS

Om du vill se de inställningar som du kan begränsa går du till [Inställningar för iOS- och iPadOS-enheter för att tillåta eller begränsa funktioner](../configuration/device-restrictions-ios.md).

#### <a name="troubleshooting-pending-mam-policy-notification-changed-to-informational-icon--6348954---"></a>Felsökning: Väntande MAM-principmeddelande ändrades till informationsikon<!--6348954 -->
Meddelandeikonen för en väntande MAM-princip på felsökningsbladet har ändrats till en informationsikon.

####  <a name="ui-update-when-configuring-compliance-policy---3961639------"></a>Uppdatering av användargränssnittet vid konfiguration av efterlevnadsprinciper<!-- 3961639    -->

Vi har uppdaterat gränssnittet för att [skapa efterlevnadsprinciper](../protect/create-compliance-policy.md#create-the-policy) i Microsoft Endpoint Manager (**Enheter** > **Efterlevnadsprinciper** > **Principer** > **Skapa princip**). Vi har en ny användarupplevelse som inkluderar samma inställningar och information som du har använt tidigare. Den nya upplevelsen följer en guideliknande process för skapande av efterlevnadsprincip och innehåller den sida där du lägger till *Tilldelningar* för principen och en *Granska + Skapa*-sida, där du kan granska konfigurationen innan du skapar principen.

#### <a name="retire-noncompliant-devices---1827291---------"></a>Ta icke-kompatibla enheter ur bruk<!-- 1827291       -->
Vi har lagt till en ny åtgärd för icke-kompatibla enheter som du kan lägga till i en princip, för att [ta icke-kompatibel enhet ur bruk](../protect/actions-for-noncompliance.md#add-actions-for-noncompliance).  Den nya åtgärden, **Ta icke-kompatibel enhet ur bruk**, innebär att alla företagsdata tas bort från enheten och att enheten inte kan hanteras av Intune.  Den här åtgärden körs när det konfigurerade värdet i dagar nås och vid det här tillfället blir enheten berättigad att tas ur bruk. Minsta värde är 30 dagar.  Explicit IT-administratörsgodkännande kommer att krävas för att dra tillbaka enheterna med hjälp av avsnittet *Dra tillbaka icke-kompatibla enheter*, där administratörer kan dra tillbaka alla berättigade enheter.

#### <a name="support-for-wpa-and-wpa2-in-ios-enterprise-wi-fi-profiles--6215273-----"></a>Stöd för WPA och WPA2 i iOS Enterprise Wi-Fi-profiler<!--6215273   -->
[Enterprise Wi-Fi-profiler för iOS](../configuration/wi-fi-settings-ios.md#enterprise-profiles) har nu stöd för fältet *Säkerhetstyp*. För *Säkerhetstyp* kan du välja antingen **WPA Enterprise** eller **WPA/WPA2 Enterprise**, och sedan ange ett val för *EAP-typ*.  (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** och välj **iOS/iPad** för *Platform* och **Wi-Fi** för *Profil*). 

De nya företagsalternativen är som de som har varit tillgängliga för en enkel Wi-Fi-profil för iOS.

#### <a name="new-user-experience-for-certificate-email-vpn-and-wi-fi-vpn-profiles---5615208-----"></a>Ny användarupplevelse för certifikat, e-post, VPN, Wi-Fi, och VPN-profiler<!-- 5615208   -->
Vi har uppdaterat [användarupplevelsen](../configuration/device-profile-create.md) i administrationscentret för slutpunktshantering (**Enheter** > **Konfigurationsprofiler** > **Skapa profil**) för skapande och ändring av följande profiltyper. Den nya upplevelsen visar samma inställningar som tidigare men använder en guideliknande upplevelse som inte kräver lika mycket horisontell rullning. Du behöver inte ändra befintliga konfigurationer med den nya upplevelsen.

- Härledd autentiseringsuppgift
- E-post
- PKCS-certifikat
- PKCS-importerat certifikat
- SCEP-certifikat
- Betrott certifikat
- VPN
- Wi-Fi

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Enhetsregistrering

#### <a name="configure-if-enrollment-is-available-in-company-portal-for-android-and-ios---4260128----"></a>Konfigurera huruvida registrering är tillgänglig i Företagsportal för Android och iOS<!-- 4260128  -->
Du kan konfigurera huruvida enhetsregistrering i Företagsportal på enheter med Android eller iOS är tillgänglig med prompter, tillgänglig utan prompter eller inte tillgänglig för användare. Du hittar de här inställningarna i Intune genom att gå till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) och välja **Administration av klientorganisation** > **Anpassning** > **Redigera** > **Enhetsregistrering**.  

Stöd för inställningen för enhetsregistrering kräver att slutanvändarna har följande Företagsportal-versioner:
-    Företagsportal på iOS: version 4.4 eller senare
-    Företagsportal på Android: version 5.0.4715.0 eller senare

Mer information om befintlig anpassning av Företagsportal finns i [Så här konfigurerar du Microsoft Intune-företagsportalappen](../apps/company-portal-app.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Enhetshantering

#### <a name="new-android-report-on-android-devices-overview-page---5435435-----"></a>Ny Android-rapport på översiktssidan för Android-enheter<!-- 5435435   -->
Vi har lagt till en rapport i Microsoft Endpoint Manager-administratörskonsolen på översiktssidan för Android-enheter. Där visas hur många Android-enheter som har registrerats i varje lösning för enhetshantering. Det här diagrammet (liksom samma diagram som redan finns i Azure-konsolen) visar antal arbetsprofilenheter samt fullständigt hanterade, dedikerade och enhetsadministratörsregistrerade enheter. Om du vill se rapporten väljer du **Enheter** > **Android** > **Översikt**.

#### <a name="guide-users-from-android-device-administrator-management-to-work-profile-management--5857738-----"></a>Vägled användare från administratörshantering av Android-enheter till arbetsprofilhantering<!--5857738   -->
Vi släpper en ny efterlevnadsinställning för administratörsplattformen för Android-enheter. Med den här inställningen kan du göra en enhet icke-kompatibel om den hanteras med enhetsadministratör.

På dessa icke-kompatibla enheter kommer användare att på sidan **Uppdatera enhetsinställningar** se meddelandet **Flytta till konfiguration av enhetshantering**. Om de trycker på knappen **Lös** vägleds de genom:

1. Avregistrering från enhetsadministratörshantering
2. Registrering i arbetsprofilhantering
3. Lösa efterlevnadsproblem 
 
Google minskar stödet för enhetsadministration i nya versioner av Android för att kunna övergå till en modern, mer omfattande och säkrare enhetshantering med Android Enterprise.  Intune kan endast erbjuda fullt stöd för enhetsadministratörshanterade Android-enheter som kör Android 10 och senare till och med andra kvartalet 2020. Enhetsadministratörshanterade enheter (förutom Samsung) som kör Android 10 eller senare efter denna tidpunkt kommer inte längre att kunna hanteras fullt ut. Det innebär exempelvis att berörda enheter inte får de nya lösenordskraven.

Mer information om den här inställningen finns i [Flytta Android-enheter från enhetsadministratören till arbetsprofilhantering](../enrollment/android-move-device-admin-work-profile.md). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Övervaka och felsöka

#### <a name="the-data-warehouse-now-provides-the-mac-address---6123680----"></a>Data Warehouse tillhandahåller nu MAC-adressen<!-- 6123680  -->
Intune Data Warehouse tillhandahåller MAC-adressen som en ny egenskap (`EthernetMacAddress`) i entiteten `device` så att administratörer kan korrelera mellan användaren och Mac-adressen. Den här egenskapen hjälper till att komma åt vissa användare och felsöka incidenter som inträffar i nätverket. Administratörer kan också använda den här egenskapen i [Power BI-rapporter](../developer/reports-proc-get-a-link-powerbi.md) för att skapa mer omfattande rapporter. Mer information finns i Intune Data Warehouse-[enheten](../developer/intune-data-warehouse-collections.md#devices).

#### <a name="additional-data-warehouse-device-inventory-properties---6125732----"></a>Ytterligare egenskaper för Data Warehouse-enhetsinventering<!-- 6125732  -->
Ytterligare egenskaper för enhetsinventering är tillgängliga via Intune Data Warehouse. Följande egenskaper är nu tillgängliga via betasamlingen [devices](../developer/reports-ref-devices.md#devices):
- `ethernetMacAddress` – den unika nätverksidentifieraren för den här enheten.
- `model` – enhetsmodellen.
- `office365Version` – den version av Office 365 som är installerad på enheten.
- `windowsOsEdition` – operativsystemversionen.

Följande egenskaper är nu tillgängliga via betasamlingen [devicepropertyHistory](../developer/reports-ref-devices.md#devicepropertyhistories):
- `physicalMemoryInBytes` – fysiskt minne i bytes.
- `totalStorageSpaceInBytes` – Total lagringskapacitet i bytes.

Mer information finns i [Microsoft Intune-API:et Data Warehouse](../developer/reports-nav-intune-data-warehouse.md).

#### <a name="help-and-support-workflow-update-to-support-additional-services---5654170-----"></a>Uppdatering av arbetsflöde för hjälp och support för att stödja ytterligare tjänster<!-- 5654170   -->
Vi har uppdaterat sidan Hjälp och support i administrationscentret för Microsoft Endpoint Manager där du nu [väljer den hanteringstyp som du använder](../fundamentals/get-support.md#options-to-access-help-and-support). Med den här ändringen kommer du att kunna välja bland följande hanteringstyper:

- Configuration Manager (inkluderar Desktop Analytics)
- Intune
- Samhantering

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="security"></a>Säkerhet

#### <a name="use-a-preview-of-security-administrator-focused-policies-as-part-of-endpoint-security--6131401----"></a>Använd en förhandsversion med principer fokuserade på säkerhetsadministratören som en del av slutpunktssäkerheten<!--6131401  -->
Som en offentlig förhandsversion har vi lagt till flera nya principgrupper under noden för slutpunktssäkerhet i administrationscentret för Microsoft Endpoint Management. Som säkerhetsadministratör kan du använda de här nya principerna för att fokusera på vissa aspekter av enhetssäkerhet för att hantera diskreta grupper av relaterade inställningar utan att den större delen av enhetskonfigurationsprinciper används.

Med undantag för den nya *Antivirusprincipen för Microsoft Defender Antivirus* (se nedan), är inställningarna i var och en av de här nya förhandsversionsprinciperna och -profilerna samma inställningar som du kanske redan konfigurerar via [enhetskonfigurationsprofiler](../configuration/device-profile-create.md) idag.

Följande är de nya principtyperna som är tillgängliga i förhandsversionen och deras tillgängliga profiltyper:

- **Antivirusprogram (förhandsversion)** :
  - macOS:
    - **Antivirus** – hantera [Principinställningar för Antivirus](../protect/antivirus-microsoft-defender-settings-macos.md) för macOS för att hantera [Microsoft Defender ATP för Mac](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac).

  - Windows 10 och senare:
    - **Microsoft Defender Antivirus** – hantera [Principinställningar för Antivirus](../protect/antivirus-microsoft-defender-settings-windows.md) för molnskydd, antivirusundantag, reparation, genomsökningsalternativ med mera.

      Antivirusprofilen för *Microsoft Defender Antivirus* är ett undantag som introducerar en ny instans av inställningar som finns som en del av en enhetsbegränsningsprofil. De här nya antivirusinställningarna:

        - Är samma inställningar som finns i enhetsbegränsningar, men har stöd för ett tredje alternativ för konfiguration som inte är tillgängligt när de har konfigurerats som en enhetsbegränsning.
        - Gäller för enheter som är samhanterade med Configuration Manager när [skjutreglaget för arbetsbelastning](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads) för samhantering av Endpoint Protection har angetts till Intune.

     Planerar att använda den nya *Antivirus* > *Microsoft Defender Antivirus*-profilen i stället för att konfigurera dem via en enhetsbegränsningsprofil.

  - **Windows-säkerhetsupplevelse** – Hantera Windows-säkerhetsinställningar som slutanvändare kan visa i Microsoft Defender Security Center och vilka meddelanden de får. De här inställningarna är oförändrade från de som är tillgängliga som en Endpoint Protection-profil för enhetskonfiguration.

- **Diskkryptering (förhandsversion)** :
  - macOS:
    - **FileVault**
  - Windows 10 och senare:
    - **BitLocker**
- **Brandvägg (förhandsversion)** :
  - macOS:
    - **macOS-brandvägg**
  - Windows 10 och senare:
    - **Microsoft Defender-brandväggen**
- **Slutpunktsidentifiering och svar (förhandsgranskning)** :
  - Windows 10 och senare: -**Windows 10 Intune**
- **Minskning av attackytan (förhandsversion)** :
  - Windows 10 och senare:
    - **App- och webbläsarisolering**
    - **Webbskydd**
    - **Programregleringstyp**
    - **Regler för att minska attackytan**
    - **Enhetskontroll**
    - **Sårbarhetsskydd**
- **Kontoskydd (förhandsversion)** :
  - Windows 10 och senare:
    - **Kontoskydd**

<!-- ########################## -->
## <a name="week-of-march-9-2020"></a>Den vecka som börjar 9 mars 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Apphantering

#### <a name="configure-delivery-optimization-agent-when-downloading-win32-app-content---5410945---"></a>Konfigurera leveransoptimeringsagent vid nedladdning av Win32-appinnehåll<!-- 5410945 -->

Du kan konfigurera att leveransoptimeringsagenten laddar ned Win32-appinnehåll, antingen i bakgrunds- eller förgrundsläge baserat på tilldelning. För befintliga Win32-appar fortsätter innehållet att laddas ned i bakgrundsläge. I [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) väljer du **Appar** > **Alla appar** > *Win32-appen* > **Egenskaper**. Välj **Redigera** bredvid **Tilldelningar**.  Redigera tilldelningen genom att välja **Inkludera** under **Läge** i avsnittet **Krävs**.  Du hittar den nya inställningen i avsnittet **Appinställningar**. Mer information om leveransoptimering finns i [Win32-apphantering – Leveransoptimering](../apps/apps-win32-app-management.md#delivery-optimization).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Enhetshantering

#### <a name="change-primary-user-for-windows-devices---3794742-----"></a>Ändra primär användare för Windows-enheter<!-- 3794742   -->
Du kan ändra den primära användaren för Windows-hybridanslutna och Azure AD-anslutna enheter. Om du vill göra det går du till **Intune** > - **Enheter** > **Alla enheter** > väljer en enhet > **Egenskaper** > **Primär användare**. Mer information finns i [Ändra en enhets primära användare](../remote-actions/find-primary-user.md#change-a-devices-primary-user).

En ny RBAC-behörighet (Hanterade enheter/ange primär användare) har också skapats för den här uppgiften. Behörigheten har lagts till i inbyggda roller som supportavdelning, skoladministratör och slutpunktssäkerhetshanterare.

Den här funktionen distribueras till kunder globalt som en förhandsversion. Du bör se funktionen inom de närmaste veckorna.


<!-- ########################## -->
## <a name="week-of-march-2-2020"></a>Den vecka som börjar 2 mars 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Enhetshantering

#### <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions---6317104-cm3555758--"></a>Ansluta Microsoft Endpoint Manager-klientorganisation: Enhetssynkronisering och enhetsåtgärder<!-- 6317104, CM3555758-->
Microsoft Endpoint Manager sammanfogar Configuration Manager och Intune i en enda konsol. Från och med den tekniska förhandsversionen av Configuration Manager version 2002.2 kan du ladda upp dina Configuration Manager-enheter till molntjänsten och vidta åtgärder i administrationscentret. Mer information finns i [Funktioner i den tekniska förhandsversionen av Configuration Manager version 2002.2](https://docs.microsoft.com/configmgr/core/get-started/2020/technical-preview-2002-2#bkmk_attach).

Läs artikeln om [den tekniska förhandsversionen av Configuration Manager](https://docs.microsoft.com/configmgr/core/get-started/technical-preview) innan du installerar uppdateringen. I artikeln beskrivs de allmänna kraven och begränsningarna för att använda en teknisk förhandsversion, hur du uppdaterar mellan versioner och hur du ger feedback.

#### <a name="bulk-remote-actions--4576882--"></a>Massfjärråtgärder<!--4576882-->
Nu kan du utfärda masskommandon för följande fjärråtgärder: starta om, byt namn på, autopilot-återställning, rensning och borttagning. Om du vill se de nya massåtgärderna går du till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Enheter** > **Alla enheter** > **Massåtgärder**.

#### <a name="all-devices-list-improved-search-sort-and-filter--6179023--"></a>Listan Alla enheter har förbättrad sökning, sortering och filtrering<!--6179023-->
Prestanda, sökning, sortering och filtrering har förbättrats för listan Alla enheter. Mer information finns i [detta supporttips](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-changes-in-all-devices-list-and-reporting-in-intune/ba-p/1220946).  

### <a name="app-management"></a>Apphantering  
####  <a name="improved-sign-in-experience-in-company-portal-for-android"></a>Förbättrad inloggningsupplevelse i Företagsportal för Android    
Vi har uppdaterat layouten för flera inloggningsskärmar i företagsportalappen för Android så att upplevelsen blir modernare, enklare och tydligare för användare. En titt på förbättringarna finns i [Nyheter i användargränssnittet för appen](https://docs.microsoft.com/mem/intune/fundamentals/whats-new-app-ui).

<!-- ########################## -->
## <a name="week-of-february-24-2020"></a>Den vecka som börjar den 24 februari 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Apphantering

#### <a name="macos-company-portal-user-experience-improvements---5568987---"></a>Förbättringar av användarupplevelsen i företagsportalen för macOS<!-- 5568987 -->
Vi har förbättrat registreringsupplevelsen för macOS-enheter och företagsportalappen för Mac. Du kommer att se följande förbättringar:
- En bättre Microsoft **AutoUpdate**-upplevelse under registreringen som ser till att användarna har den senaste versionen av företagsportalen.
- En bättre kompatibilitetskontroll under registreringen.
- Stöd för kopierade incident-ID:n så att användarna snabbare kan skicka fel från sina enheter till företagets supportteam.

Mer information om registrering och företagsportalappen för Mac finns i [Registrera din macOS-enhet med hjälp av företagsportalappen](../user-help/enroll-your-device-in-intune-macos-cp.md).

#### <a name="app-protection-policies-for-better-mobile-now-supports-ios-and-ipados---6224512----"></a>Appskyddspolicyerna för Better Mobile har nu stöd för iOS och iPadOS<!-- 6224512  -->

I oktober 2019 utökades appskyddspolicyerna i Intune med möjligheten att använda data från Microsoft Threat Defense-partner. Den här uppdateringen gör att du kan använda en appskyddspolicy till att blockera eller selektivt rensa användarnas företagsdata baserat på hälsotillståndet för enheter som använder Better Mobile i iOS och iPadOS.  Mer information finns i [Skapa en Mobile Threat Defense-appskyddsprincip med Intune](../protect/mtd-app-protection-policy.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Enhetshantering

#### <a name="exports-from-the-all-devices-list--now-in-zipped-csv-format--6343117--"></a>Nu kan du exportera från listan Alla enheter i zippat CSV-format<!--6343117-->
Exporter från sidan **Enheter** > **Alla enheter** är nu i zippat CSV-format.


<!-- ########################## -->
## <a name="week-of-february-17-2020-2002-service-release"></a>Den vecka som börjar den 17 februari 2020 (tjänstversionen 2002)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Apphantering

#### <a name="microsoft-defender-advanced-threat-protection-atp-app-for-macos---5424618---"></a>Appen Microsoft Defender Avancerat skydd (ATP) för macOS<!-- 5424618 -->
Intune tillhandahåller ett enkelt sätt att distribuera appen Microsoft Defender Avancerat skydd (ATP) för macOS till hanterade Mac-enheter. Mer information finns i [Add Microsoft Defender ATP to macOS devices using Microsoft Intune](../apps/apps-advanced-threat-protection-macos.md) (Lägga till Microsoft Defender ATP i macOS-enheter med Microsoft Intune) och [Microsoft Defender Advanced Threat Protection for Mac](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) (Microsoft Defender Avancerat skydd för Mac).  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Enhetskonfiguration

#### <a name="enable-network-access-control-nac-with-cisco-anyconnect-vpn-on-ios-devices---4860111----"></a>Aktivera nätverksåtkomstkontroll med Cisco AnyConnect VPN på iOS-enheter<!-- 4860111  -->
På iOS-enheter kan du skapa en VPN-profil och använda olika anslutningstyper, inklusive Cisco AnyConnect (**Enhetskonfiguration** > **Profiler** > **Skapa profil** > **iOS** som plattform > **VPN** som profiltyp > **Cisco AnyConnect** som anslutningstyp).

Du kan aktivera nätverksåtkomstkontroll med Cisco AnyConnect. Gör så här för att använda funktionen:

1. I [Cisco Identity Services Engine Administrator Guide](https://www.cisco.com/c/en/us/td/docs/security/ise/2-1/admin_guide/b_ise_admin_guide_21/b_ise_admin_guide_20_chapter_01000.html) använder du anvisningarna i **Configuring Microsoft Intune as an MDM Server** (Konfigurera Microsoft Intune som en MDM-server) för att konfigurera Cisco Identity Services Engine (ISE) i Azure.
2. I enhetskonfigurationsprofilen för Intune väljer du inställningen **Aktivera nätverksåtkomstkontroll**.

Om du vill se alla tillgängliga VPN-inställningar går du till [Konfigurera VPN-inställningar på iOS-enheter](../configuration/vpn-settings-ios.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Enhetsregistrering

#### <a name="serial-number-on-the-apple-mdm-push-certificate-page--5947765----"></a>Serienummer på sidan för Apple MDM-pushcertifikat<!--5947765  -->
Nu visas serienumret på sidan för Apple MDM-pushcertifikat. Serienumret behövs för att få åtkomst till Apple MDM-pushcertifikatet om åtkomsten till det Apple-ID som skapade certifikatet skulle förloras. Om du vill visa serienumret går du till **Devices (Enheter)**  > **iOS** > **iOS enrollment (iOS-registrering)**  > **Apple MDM Push certificate (Apple MDM-pushcertifikat)** .

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Enhetshantering

#### <a name="new-update-schedule-options-for-pushing-os-updates-to-enrolled-iosipados-devices--5879689----"></a>Nya alternativ för uppdateringsschemat för att skicka OS-uppdateringar till registrerade iOS/iPadOS-enheter<!--5879689  -->
Du kan använda följande alternativ när du schemalägger operativsystemsuppdateringar för iOS/iPadOS-enheter. Dessa alternativ gäller för enheter som använde registreringstypen Apple Business Manager eller Apple School Manager.
- Uppdatera vid nästa incheckning
- Uppdatera under schemalagd tid
- Uppdatera utanför schemalagd tid

För de två sista alternativen kan du skapa flera tidsperioder.

Om du vill se de nya alternativen går du till MEM > **Devices (Enheter)**  > **iOS** > **Update policies for iOS/iPadOS (Uppdateringsprinciper för iOS/iPadOS)**  > **Create profile (Skapa profil)** .

#### <a name="choose-which-iosipados-updates-to-push-to-enrolled-devices--5879689----"></a>Välja vilka iOS/iPadOS-uppdateringar som ska skickas till registrerade enheter<!--5879689  -->
Du kan välja en specifik iOS/iPadOS-uppdatering (med undantag för den senaste uppdateringen) som ska skickas till enheter som har registrerats med hjälp av antingen Apple Business Manager eller Apple School Manager. För dessa enheter måste en enhetskonfigurationsprincip anges för att fördröja programuppdateringens synlighet ett antal dagar. Om du vill se den här funktionen går du till MEM > **Devices (Enheter)**  > **iOS** > **Update policies for iOS/iPadOS (Uppdateringsprinciper för iOS/iPadOS)**  > **Create profile (Skapa profil)** .



<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Enhetssäkerhet

#### <a name="improved-intune-reporting-experience---3791418-----"></a>Förbättrad rapporteringsupplevelse i Intune<!-- 3791418   -->
Intune har nu en förbättrad rapporteringsupplevelse, inklusive nya rapporttyper, bättre rapportorganisation, mer fokuserade vyer, förbättrade rapportfunktioner samt mer konsekventa och tidsrelevanta data. Rapporteringsupplevelsen kommer att flyttas från allmänt tillgänglig förhandsversion till GA (allmän tillgänglighet). Dessutom tillhandahåller GA-versionen lokaliseringsstöd, felkorrigeringar, designförbättringar och aggregerade enhetsefterlevnadsdata på paneler i [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

De nya rapporttyperna fokuserar på följande information:

- **Drift** – tillhandahåller färska poster med fokus på driftproblem. 
- **Organisation** – innehåller en bred sammanfattning av det övergripande läget.
- **Historisk** – visar mönster och trender under en viss tidsperiod.
- **Specialist** – låter dig använda rådata för att skapa dina egna anpassade rapporter.

Den första uppsättningen nya rapporter fokuserar på enhetsefterlevnad. Mer information finns i [Blogg – Rapporteringsramverk i Microsoft Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/New-Reporting-Framework-Coming-to-Intune/ba-p/1009553) och [Intune-rapporter](reports.md).

#### <a name="consolidated-the-location-of-security-baselines-in-the-ui---6177074-----"></a>Platsen för säkerhetsbaslinjer i användargränssnittet har konsoliderats<!-- 6177074   -->
Vi har konsoliderat sökvägarna till [säkerhetsbaslinjer](../protect/security-baselines.md) i administrationscentret för Microsoft Endpoint Manager genom att ta bort *Säkerhetsbaslinjer* från flera platser i användargränssnittet. Nu använder du följande sökväg för att nå säkerhetsbaslinjer:  **Slutpunktssäkerhet** > **Säkerhetsbaslinjer**.

#### <a name="expanded-support-for-imported-pkcs-certificates---6044197----"></a>Utökat stöd för importerade PKCS-certifikat<!-- 6044197  -->
Vi har utökat stödet för användning av [importerade PKCS-certifikat](../protect/certificates-imported-pfx-configure.md#supported-platforms) för att stödja *fullständigt hanterade Android Enterprise-enheter*. Normalt används import av PFX-certifikat för S/MIME-krypteringsscenarier, där användaren måste ha krypteringscertifikat på alla sina enheter för att e-postkrypteringen ska kunna utföras.

Import av PFX-certifikat stöds för följande plattformar:

- Android – enhetsadministratör
- Android Enterprise – fullständigt hanterad
- Android Enterprise – arbetsprofil
- iOS
- Mac
- Windows 10

#### <a name="view-the-endpoint-security-configuration-for-devices---6206460----"></a>Visa konfiguration av slutpunktssäkerhet för enheter<!-- 6206460  -->
Vi har ändrat namnet på det alternativ i administrationscentret för Microsoft Endpoint Manager som visar de [slutpunktssäkerhetsinställningar som gäller för en viss enhet](../protect/security-baselines-monitor.md#view-endpoint-security-configurations-per-device). Namnet på det här alternativet har ändrats till **Konfiguration av slutpunktssäkerhet** eftersom det visar tillämpliga säkerhetsbaslinjer och ytterligare principer som skapats utanför säkerhetsbaslinjerna. Tidigare hette det här alternativet *Säkerhetsbaslinjer*.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Rollbaserad åtkomstkontroll

#### <a name="intune-roles-user-interface-changes-coming--5801612-----"></a>Användargränssnittsändringar i Intune-roller kommer<!--5801612   -->
Användargränssnittet för [Microsoft Endpoint Manager-administrationscenter](https://go.microsoft.com/fwlink/?linkid=2109431) > **Administration av klientorganisation** > **Roller** har fått en mer användarvänlig och intuitiv design. De här funktionerna tillhandahåller samma inställningar och information som du använder nu, men de nya funktionerna använder en guideliknande process.

<!-- ########################## -->
## <a name="week-of-february-17-2020"></a>Den vecka som börjar den 17 februari 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Apphantering

#### <a name="microsofts-new-office-app---5859926---"></a>Microsofts nya Office-app<!-- 5859926 -->
Microsofts nya Office-app är nu allmänt tillgänglig för hämtning och användning. Med Office-appen kan du arbeta i Word, Excel och PowerPoint från en enda app. Du kan använda en appskyddsprincip för appen för att skydda åtkomsten till data.

Mer information finns i [How to enable Intune app protection policies with the Office mobile preview app](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-how-to-enable-intune-app-protection-policies-with/ba-p/1045493) (Aktivera appskyddsprinciper i Intune med förhandsversionen av Office-appen).

<!-- ########################## -->

## <a name="week-of-february-10-2020"></a>Den vecka som börjar den 10 februari 2020

### <a name="windows-7-ends-extended-support--3042987---"></a>Utökad support för Windows 7 avslutas<!--3042987 -->
Utökad support för Windows 7 avslutades den 14 januari 2020. Inaktuella Intunes stöd för enheter som kör Windows 7 avslutas på samma gång. Teknisk hjälp och automatiska uppdateringar som hjälper till att skydda din dator är inte längre tillgängliga. Du bör uppgradera till Windows 10. Mer information finns i blogginlägget [Planera för förändring](https://aka.ms/Windows7_Intune).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Apphantering

#### <a name="microsoft-edge-version-77-and-later-on-windows-10-devices---5843584---"></a>Microsoft Edge version 77 och senare på Windows 10-enheter<!-- 5843584 -->
Intune stöder nu avinstallation av Microsoft Edge version 77 och senare på Windows 10-enheter. Mer information finns i [Lägga till Microsoft Edge för Windows 10 till Microsoft Intune](../apps/apps-windows-edge.md).

#### <a name="screen-removed-from-company-portal-android-work-profile-enrollment--6103987---"></a>En skärm har tagits bort från registreringen av Android-arbetsprofiler i företagsportalen<!--6103987 -->
Skärmen **Vad händer nu?** har tagits bort från registreringsflödet för Android-arbetsprofiler i företagsportalen för att effektivisera användarupplevelsen. Gå till [Registrera med Android-arbetsprofilen](../user-help/enroll-device-android-work-profile.md) om du vill se det uppdaterade registreringsflödet för Android-arbetsprofiler.  

#### <a name="company-portal-app-improved-performance---6178652---"></a>Förbättrade prestanda för Företagsportal-appen<!-- 6178652 -->
Företagsportal-appen har uppdaterats för att ge stöd för förbättrade prestanda för enheter som använder ARM64-processorer, t.ex. Surface Pro X. Tidigare använde Företagsportal ett emulerat ARM32-läge. Nu kompileras Företagsportal-appen, i version 10.4.7080.0 och senare, internt för ARM64. Mer information om Företagsportal-appen finns i [Så här konfigurerar du Microsoft Intune-företagsportalsappen](../apps/company-portal-app.md).

## <a name="whats-new-archive"></a>Nyhetsarkiv
Information om tidigare månader finns i [Nyhetsarkiv](whats-new-archive.md).

## <a name="notices"></a>Meddelanden

[!INCLUDE [Intune notices](../includes/intune-notices.md)]


