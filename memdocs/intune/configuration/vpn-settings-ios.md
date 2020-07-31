---
title: Konfigurera VPN-inställningar för iOS/iPadOS-enheter i Microsoft Intune – Azure | Microsoft Docs
description: Lägg till eller skapa en VPN-konfigurationsprofil på iOS/iPadOS-enheter med inställningar för virtuellt privat nätverk (VPN). Konfigurera anslutningsinformation, autentiseringsmetoder, delade tunnlar, anpassade VPN-inställningarna med identifieraren, nyckel- och värdepar, VPN-inställningarna per app som inkluderar Safari-webbadresser och VPN-anslutningar på begäran med SSID- eller DNS-sökningsdomäner, proxyinställningar för att inkludera ett konfigurationsskript, en IP- eller FQDN-adress och en TCP-port i Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/08/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: e74817c21f7869fdfdabcc2947766b5af9dea335
ms.sourcegitcommit: 19f5838eb3eb8724d22382f36f9564ac9a978b97
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/29/2020
ms.locfileid: "87365499"
---
# <a name="add-vpn-settings-on-ios-and-ipados-devices-in-microsoft-intune"></a>Lägg till VPN-inställningar på iOS- och iPadOS-enheter i Microsoft Intune

Microsoft Intune innehåller många VPN-inställningar som kan distribueras till iOS/iPadOS-enheter. De här inställningarna används för att skapa och konfigurera VPN-anslutningar till din organisations nätverk. Den här artikeln beskriver dessa inställningar. Vissa inställningar är bara tillgängliga för vissa VPN-klienter, till exempel Citrix och Zscaler.

## <a name="before-you-begin"></a>Innan du börjar

[Skapa en enhetskonfigurationsprofil](vpn-settings-configure.md).

> [!NOTE]
> De här inställningarna är tillgängliga för alla registreringstyper med undantag för användarregistrering. Användarregistreringen är begränsad till [per app-VPN](/vpn-setting-configure-per-app.md). Mer information om de olika registreringstyperna finns i [iOS/iPadOS-registrering](../enrollment/ios-enroll.md).

## <a name="connection-type"></a>Anslutningstyp

Välj VPN-anslutningstypen från följande leverantörslista:

- **Check Point Capsule VPN**
- **Cisco Legacy AnyConnect**: Gäller för [Cisco Legacy AnyConnect](https://itunes.apple.com/app/cisco-legacy-anyconnect/id392790924)-appversion 4.0.5x och tidigare.
- **Cisco AnyConnect**: Gäller för [Cisco AnyConnect](https://itunes.apple.com/app/cisco-anyconnect/id1135064690)-appversion 4.0.7x och senare.
- **SonicWall Mobile Connect**
- **F5 Access Legacy**: Gäller för F5 Access-appversion 2.1 och tidigare.
- **F5 Access**: Gäller för F5 Access-appversion 3.0 och senare.
- **Palo Alto Networks GlobalProtect (äldre)** : Gäller för Palo Alto Networks GlobalProtect-appversion 4.1 och tidigare.
- **Palo Alto Networks GlobalProtect**: Gäller för Palo Alto Networks GlobalProtect-appversion 5.0 och tidigare.
- **Pulse Secure**
- **Cisco (IPSec)**
- **Citrix VPN**
- **Citrix SSO**
- **Zscaler**: Om du vill använda Villkorsstyrd åtkomst eller tillåta att användarna hoppar över Zscaler-inloggningsskärmen måste du integrera Zscaler Private Access (ZPA) med ditt Azure AD-konto. Detaljerade anvisningar finns i [Zscaler-dokumentationen](https://help.zscaler.com/zpa/configuration-guide-microsoft-azure-ad).
- **IKEv2**: [IKEv2-inställningar](#ikev2-settings) (i den här artikeln) beskriver egenskaperna.
- **Anpassat VPN**

> [!NOTE]
> Cisco, Citrix, F5 och Palo Alto har tillkännagivit att deras äldre klienter inte fungerar i iOS 12. Du bör migrera till de nya apparna så snart som möjligt. Mer information finns i [Microsoft Intune-supportteamets blogg](https://go.microsoft.com/fwlink/?linkid=2013806&clcid=0x409).

## <a name="base-vpn-settings"></a>Grundläggande VPN-inställningar

De inställningar som visas i följande lista bestäms av den VPN-anslutningstyp som du väljer.  

- **Anslutningens namn**: Slutanvändarna ser det här namnet när de bläddrar i en lista över tillgängliga VPN-anslutningar på enheten.
- **Anpassat domännamn** (endast Zscaler): Fyll i Zscaler-appens inloggningsfält på förhand med den domän som användarna tillhör. Om ett användarnamn exempelvis är `Joe@contoso.net`, kommer domänen `contoso.net` att visas statiskt i fältet när appen öppnas. Om du inte anger ett domännamn används domändelen av UPN-namnet i Azure Active Directory (AD).
- **IP-adress eller fullständigt domännamn**: IP-adressen eller det fullständiga domännamnet för VPN-servern som enheterna ska ansluta till. Ange till exempel `192.168.1.1` eller `vpn.contoso.com`.
- **Organisationens molnnamn** (endast Zscaler): Ange namnet på det moln där din organisation har etablerats. URL:en som du använder för att logga in till Zscaler innehåller namnet.  
- **Autentiseringsmetod**: Välj hur enheter autentiserar mot VPN-servern. 
  - **Certifikat**: Under **Autentiseringscertifikat** väljer du en befintlig SCEP- eller PKCS-certifikatprofil för att autentisera anslutningen. [Konfigurera certifikat](../protect/certificates-configure.md) innehåller vägledning om certifikatprofiler.
  - **Användarnamn och lösenord**: Slutanvändare måste ange ett användarnamn och ett lösenord för att logga in på VPN-servern.  

    > [!NOTE]
    > Om användarnamnet och lösenordet används som autentiseringsmetod för Cisco IPsec VPN, måste de ge SharedSecret via en anpassad profil i Apple Configurator.

  - **Härledd autentiseringsuppgift**: Använd ett certifikat som härletts från en användares smartkort. Om ingen utfärdare av härledd autentiseringsuppgift har konfigurerats, kommer Intune att be dig lägga till en. Mer information finns i [Använd härledda autentiseringsuppgifter i Microsoft Intune](../protect/derived-credentials.md).

- **Undantagna webbadresser** (endast Zscaler): Vid anslutning till Zscaler VPN är de angivna webbadresserna tillgängliga utanför Zscaler-molnet. 

- **Delade tunnlar**: **Aktivera** eller **Inaktivera** för att låta enheterna bestämma vilken anslutning som ska användas beroende på trafiken. En användare på ett hotell kan till exempel använda VPN-anslutningen för att komma åt arbetsfiler, men använda hotellets standardnätverk för vanlig webbsurfning.

- **VPN-id** (anpassat VPN, Zscaler och Citrix): En identifierare för VPN-appen som du använder och som tillhandahålls av VPN-leverantören.
- **Ange nyckel/värde-par för organisationens anpassade VPN-attribut** (anpassat VPN, Zscaler och Citrix): Lägg till eller importera **nycklar** och **värden** som anpassar VPN-anslutningen. Glöm inte att dessa värden vanligtvis tillhandahålls av VPN-leverantören.

- **Aktivera nätverksåtkomstkontroll (NAC)** (Cisco AnyConnect, Citrix SSO, F5 Access): När du väljer **Jag accepterar** tas det här enhets-ID:t med i VPN-profilen. Detta ID kan användas för VPN-autentisering för att tillåta eller förhindra nätverksåtkomst.

  **Vid användning av Cisco AnyConnect med ISE** bör du se till att:

  - Om du inte redan har gjort det, integrerar du ISE med Intune för NAC enligt beskrivningen i **Konfigurera Microsoft Intune som en MDM-server** i [administratörsguiden för Cisco Identity Services Engine](https://www.cisco.com/c/en/us/td/docs/security/ise/2-1/admin_guide/b_ise_admin_guide_21/b_ise_admin_guide_20_chapter_01000.html).
  - Aktivera NAC i VPN-profilen.

  **När du använder Citrix SSO med Gateway** så var noga med att:

  - Bekräfta att du använder Citrix Gateway 12.0.59 eller senare.
  - Bekräfta att dina användare har Citrix SSO 1.1.6 eller senare installerat på sina enheter.
  - Integrera Citrix Gateway med Intune för NAC. Se Citrix-distributionsguiden [Integrating Microsoft Intune/Enterprise Mobility Suite with NetScaler (LDAP+OTP Scenario)](https://www.citrix.com/content/dam/citrix/en_us/documents/guide/integrating-microsoft-intune-enterprise-mobility-suite-with-netscaler.pdf) (Integrera Microsoft Intune/Enterprise Mobility Suite med NetScaler (LDAP+OTP-scenario)).
  - Aktivera NAC i VPN-profilen.

  **När du använder F5-åtkomst** måste du se till att:

  - Bekräfta att du använder F5 BIG-IP 13.1.1.5 eller senare. 
  - Integrera BIG-IP med Intune för NAC. Läs F5-guiden [Overview: Configuring APM for device posture checks with endpoint management systems](https://support.f5.com/kb/en-us/products/big-ip_apm/manuals/product/apm-client-configuration-7-1-6/6.html#guid-0bd12e12-8107-40ec-979d-c44779a8cc89) (Översikt: Konfigurera APM för enhetsstatuskontroller med slutpunktshanteringssystem).
  - Aktivera NAC i VPN-profilen.

  För VPN-partner som stöder enhets-ID kan VPN-klienten, till exempel Citrix SSO, hämta ID:t. Sedan kan den skicka en fråga till Intune för att bekräfta att enheten är registrerad, och om VPN-profilen är kompatibel eller inte.

  - Om du vill ta bort den här inställningen återskapar du profilen och markerar inte **Jag accepterar**. Tilldela sedan profilen på nytt.

## <a name="ikev2-settings"></a>IKEv2-inställningar

Dessa inställningar gäller när du väljer **Anslutningstyp** > **IKEv2**.

- **Konstant VPN-anslutning**: **Aktivera** konfigurerar en konstant VPN-klient som automatiskt ansluter och återansluter till VPN. VPN-anslutningar som alltid är aktiva är alltid anslutna eller ansluter direkt när användaren låser sin enhet, när enheten startas om eller när det trådlösa nätverket ändras. När inställt till **Inaktivera** (standard) är Always-on VPN för alla VPN-klienter inaktiverat. När läget är aktiverat konfigurerar du även:

  - **Nätverksgränssnitt**: Alla IKEv2-inställningar gäller endast för det nätverksgränssnitt som du väljer. Alternativen är:
    - **Wifi och mobilnät** (standard): IKEv2-inställningarna gäller för Wi-Fi-och mobilgränssnittet på enheten.
    - **Mobilnät**: IKEv2-inställningarna gäller endast för mobilgränssnittet på enheten. Välj det här alternativet om du distribuerar till enheter där Wi-Fi-gränssnittet är inaktiverat eller borttaget.
    - **Trådlöst**: IKEv2-inställningarna gäller endast för Wi-Fi-gränssnittet på enheten.
  - **Användare ska inaktivera VPN-konfiguration**: **Aktivera** låter användare stänga av Always-on VPN. **Inaktivera** (standard) förhindrar att användare stänger av den. Standardvärdet för den här inställningen är det säkraste alternativet.
  - **Röstbrevlåda**: Välj vad som händer med röstbrevlådans trafik när Always-on VPN är aktiverat. Alternativen är:
    - **Tvinga nätverkstrafik via VPN** (standard): Den här inställningen är det säkraste alternativet.
    - **Tillåt nätverkstrafik att passera utanför VPN**
    - **Släpp nätverkstrafik**
  - **AirPrint**: Välj vad som händer med AirPrint-trafik när Always-on VPN är aktiverat. Alternativen är:
    - **Tvinga nätverkstrafik via VPN** (standard): Den här inställningen är det säkraste alternativet.
    - **Tillåt nätverkstrafik att passera utanför VPN**
    - **Släpp nätverkstrafik**
  - **Mobiltjänster**: På iOS 13.0+, välj vad som händer med mobiltrafik när Always-on VPN är aktiverat. Alternativen är:
    - **Tvinga nätverkstrafik via VPN** (standard): Den här inställningen är det säkraste alternativet.
    - **Tillåt nätverkstrafik att passera utanför VPN**
    - **Släpp nätverkstrafik**
  - **Tillåt trafik från icke-inbyggda nätverksprogram att passera utanför VPN**: Ett inbyggt nätverk avser Wi-Fi-hotspots som vanligtvis finns på restauranger och hotell. Alternativen är:
    - **Nej**: Tvingar all programtrafik för internt nätverk (CN) via VPN-tunneln.
    - **Ja, alla appar**: Tillåter all CN-apptrafik att kringgå VPN.
    - **Ja, särskilda appar**: **Lägg till** en lista över CN-appar vars trafik kan kringgå VPN-nätverket. Ange paketidentifierare för CN-appen. Ange till exempel `com.contoso.app.id.package`.

  - **Trafik från Captive WebSheet-app som ska passera utanför VPN**: Captive WebSheet är en inbyggd webbläsare som hanterar intern inloggning. **Aktivera** tillåter att webbläsarappens trafik kringgår VPN. **Inaktivera** (standard) framtvingar en WebSheet-trafik att använda Always-on VPN. Standardvärdet är det säkraste alternativet.
  - **Intervall för NAT (network address translation) KeepAlive (sekunder)** : För att vara ansluten till VPN-anslutningen skickar enheten nätverkspaket för att förbli aktiv. Ange ett värde i sekunder för hur ofta dessa paket skickas från 20-1440. Ange till exempel ett värde för `60` för att skicka nätverkspaketen till VPN var 60:e sekund. Det här värdet är inställt på `110` sekunder som standard.
  - **Lasta av NAT KeepAlive till maskinvara när enheten är i viloläge**: När en enhet är i strömsparläge, **Aktivera** (standard) att NAT kontinuerligt skickar Keep Alive-paket så att enheten förblir ansluten till VPN. **Inaktivera** inaktiverar den här funktionen.

- **Fjärridentifierare**: Ange nätverkets IP-adress, FQDN, UserFQDN eller ASN1DN för IKEv2-servern. Ange till exempel `10.0.0.3` eller `vpn.contoso.com`. Normalt anger du samma värde som [**Anslutningsnamnet**](#base-vpn-settings) (i den här artikeln). Men det beror på inställningarna för IKEv2-servern.

- **Typ av klientautentisering**: Välj hur VPN-klienten autentiserar till VPN. Alternativen är:
  - **Typ av användarautentisering** (standard): Autentiseringsuppgifter för användare autentiserar till VPN.
  - **Datorautentisering**: Autentiseringsuppgifter för enhet autentiserar till VPN.

- **Autentiseringsmetod**: Välj den typ av autentiseringsuppgifter för klient som ska skickas till servern. Alternativen är:
  - **Certifikat**: Använder en befintlig certifikatprofil för att autentisera till VPN. Se till att den här certifikatprofilen redan har tilldelats till användaren eller enheten. Annars misslyckas VPN-anslutningen.
    - **Certifikattyp**: Välj den typ av kryptering som ska användas av certifikatet. Se till att VPN-servern är konfigurerad för att godkänna den här typen av certifikat. Alternativen är:
      - **RSA** (standard)
      - **ECDSA256**
      - **ECDSA384**
      - **ECDSA521**

  - **Användarnamn och lösenord** (endast användarautentisering): När användare ansluter till VPN-nätverket uppmanas de att ange sitt användarnamn och lösenord.
  - **Delad hemlighet** (endast datorautentisering): Tillåter att du anger en delad hemlighet som ska skickas till VPN-servern.
    - **Delad hemlighet**: Ange den delade hemligheten, även kallat PSK (i förväg delad nyckel). Se till att värdet matchar den delade hemlighet som konfigurerats på VPN-servern.

- **Eget namn på servercertifikatutfärdare**: Tillåter att VPN-servern autentiserar till VPN-klienten. Ange certifikatutfärdarens nätverksnamn (CN) för det VPN-servercertifikat som skickas till VPN-klienten på enheten. Se till att CN-värdet matchar konfigurationen på VPN-servern. Annars misslyckas VPN-anslutningen.
- **Eget namn på servercertifikat**: Ange det egna namnet för själva certifikatet. Om inget värde anges används värdet för fjärridentifieraren.

- **DPD-frekvens (dead peer detection)** : Välj hur ofta VPN-klienten ska kontrollera om VPN-tunneln är aktiv. Alternativen är:
  - **Inte konfigurerad**: Använder iOS/iPad-systemstandarden, vilket kan vara detsamma som att välja **Medel**.
  - **Inga**: Inaktiverar DPD (dead peer detection).
  - **Låg**: Skickar ett keepalive-meddelande var 30:e minut.
  - **Medel** (standard): Skickar ett keepalive-meddelande var 10:e minut.
  - **Hög**: Skickar ett keepalive-meddelande var 60:e sekund.

- **Minimivärde för TLS-versionsintervall**: Ange den minsta TLS-version som ska användas. Ange `1.0`, `1.1`eller `1.2`. Om inget anges används standardvärdet `1.0`.
- **Maxvärde för TLS-versionsintervall**: Ange den högsta TLS-version som ska användas. Ange `1.0`, `1.1`eller `1.2`. Om inget anges används standardvärdet `1.2`.

> [!NOTE]
> TLS-versionsintervallets lägsta och högsta värde måste anges när du använder användarautentisering och certifikat.

- **Perfect Forward Secrecy**: Välj **Aktivera** för att aktivera PFS (Perfect Forward Secrecy). PFS är en funktion för IP-säkerhet som minskar påverkan om en sessionsnyckel komprometteras. **Inaktivera** (standard) använder inte PFS.
- **Certifikatåterkallningskontroll**: Välj **Aktivera** för att kontrollera att certifikaten inte återkallas innan VPN-anslutningen tillåts att lyckas. Den här kontrollen är bästa möjliga. Om VPN-servern når tidsgränsen innan du fastställer om certifikatet har återkallats, beviljas åtkomst. **Inaktivera** (standard) söker inte efter återkallade certifikat.

- **Konfigurera säkerhetskopplingsparametrar**: **Inte konfigurerat** (standard): Använder iOS/iPadOS-systemstandarden. Välj **Aktivera** för att ange de parametrar som används när du skapar säkerhetskopplingar med VPN-servern:
  - **Krypteringsalgoritm**: Välj den algoritm som du vill använda:
    - DES
    - 3DES
    - AES-128
    - AES-256 (standard)
    - AES-128-GCM
    - AES-256-GCM
  - **Integritetsalgoritm**:  Välj den algoritm som du vill använda:
    - SHA1-96
    - SHA1-160
    - SHA2-256 (standard)
    - SHA2-384
    - SHA2-512
  - **Diffie-Hellman-grupp**: Välj den grupp som du vill använda. Standardvärdet är grupp `2`.
  - **Livslängd** (minuter): Välj hur länge säkerhetskopplingen ska förbli aktiv tills nycklarna roteras. Ange ett heltal mellan `10` och `1440` (1440 minuter är 24 timmar). Standardvärdet är `1440`.

- **Konfigurera en separat uppsättning parametrar för underordnade säkerhetskopplingar**: iOS/iPad gör att du kan konfigurera separata parametrar för IKE-anslutningen och eventuella underordnade anslutningar. 

  **Inte konfigurerad** (standard) använder de värden som du anger i den tidigare inställningen **Ställ in säkerhetskopplingsparametrar**. Välj **Aktivera** för att ange de parametrar som används när du skapar *underordnade* säkerhetskopplingar med VPN-servern:
  - **Krypteringsalgoritm**: Välj den algoritm som du vill använda:
    - DES
    - 3DES
    - AES-128
    - AES-256 (standard)
    - AES-128-GCM
    - AES-256-GCM
  - **Integritetsalgoritm**:  Välj den algoritm som du vill använda:
    - SHA1-96
    - SHA1-160
    - SHA2-256 (standard)
    - SHA2-384
    - SHA2-512
  - **Diffie-Hellman-grupp**: Välj den grupp som du vill använda. Standardvärdet är grupp `2`.
  - **Livslängd** (minuter): Välj hur länge säkerhetskopplingen ska förbli aktiv tills nycklarna roteras. Ange ett heltal mellan `10` och `1440` (1440 minuter är 24 timmar). Standardvärdet är `1440`.

## <a name="automatic-vpn-settings"></a>Inställningar för automatiskt VPN

- **Per app-VPN**: Aktiverar per app-VPN. Tillåter att VPN-anslutningen aktiveras automatiskt när vissa program öppnas. Associerar även appar med den här VPN-profilen. Per app-VPN stöds inte i IKEv2. Om du vill ha mer information läser du [instruktionerna för hur du konfigurerar per app-VPN för iOS/iPadOS](vpn-setting-configure-per-app.md). 
  - **Typ av provider**: Endast tillgängligt för Pulse Secure och anpassat VPN.
  - När du använder **per app-VPN-profiler** i iOS/iPadOS med Pulse Secure eller Anpassat VPN väljer du händelsedirigering nedåt på applager (app-proxy) eller på paketnivå (paket-tunnel). Ställ in värdet **Providertyp** på **app-proxy** för händelsedirigering på appnivå eller **paket-tunnel** för händelsedirigering på paketnivå. Om du inte är säker på vilket värde du ska använda läser du VPN-leverantörens dokumentation.
  - **Safariwebbadresser som aktiverar den här VPN-anslutningen**: Lägg till en eller flera webbadresser. VPN-anslutningen upprättas automatiskt när de här webbadresserna besöks i Safari-webbläsaren på enheten.

- **VPN på begäran**: Konfigurera villkorliga regler som styr när VPN-anslutningen ska initieras. Du kan till exempel skapa ett villkor där VPN-anslutningen endast används när en enhet inte är ansluten till ett trådlöst företagsnätverk. Eller skapa ett villkor. Om en enhet till exempel inte kan komma åt en DNS-sökdomän som du har angett startas inte VPN-anslutningen.

  - **SSID:n eller DNS-sökdomäner**: Välj om det här villkoret ska använda det trådlösa nätverkets **SSID:n** eller **DNS-sökdomäner**. Välj **Lägg till** för att konfigurera en eller flera SSID:er eller sökdomäner.
  - **URL-strängavsökning**: Valfritt. Ange en URL som regeln använder som ett test. Om enheten kommer åt den här URL:en utan omdirigering, startas VPN-anslutningen. Och enheten ansluter till mål-URL:en. Användaren ser inte URL-strängens avsökningsplats.

    En URL-strängavsökning är till exempel en URL för en granskningswebbserver som kontrollerar enhetens efterlevnad innan VPN-anslutningen görs. Eller så testar webbadressen VPN-nätverkets förmåga att ansluta till en plats innan enheten ansluter till målwebbadressen via VPN.

  - **Domänåtgärd**: Välj något av följande objekt:
    - Anslut vid behov
    - Anslut aldrig
  - **Åtgärd**: Välj något av följande objekt:
    - Ansluta
    - Utvärdera anslutning
    - Ignorera
    - Koppla från

## <a name="proxy-settings"></a>Proxyinställningar

Konfigurera följande inställningar om du använder en proxyserver. Proxyinställningar är inte tillgängliga för Zscaler VPN-anslutningar.  

- **Automatiskt konfigurationsskript**: Använd en fil för att konfigurera proxyservern. Ange den **Proxyserver-URL** (till exempel `http://proxy.contoso.com`) som innehåller konfigurationsfilen.
- **Adress**: Ange IP-adressen för det fullt kvalificerade värdnamnet för proxyservern.
- **Portnummer**: Ange det portnummer som är associerat med proxyservern.

## <a name="next-steps"></a>Nästa steg

Profilen har skapats, men den gör inte något än. [Tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).

Konfigurera VPN-inställningar på [Android](vpn-settings-android.md)-, [Android Enterprise](vpn-settings-android-enterprise.md)-, [macOS](vpn-settings-macos.md)- och [Windows 10](vpn-settings-windows-10.md)-enheter.
