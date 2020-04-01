---
title: Skyddsinställningar för Windows 10-enheter i Microsoft Intune – Azure | Microsoft Docs
description: På Windows 10-enheter kan du använda eller konfigurera inställningar för slutpunktsskydd för att aktivera Microsoft Defender-funktionalitet, inklusive Application Guard, brandvägg, SmartScreen, kryptering och bitlocker, Exploit Guard, programreglering, Säkerhetscenter och säkerhet på lokala enheter i Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/13/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 3af7c91b-8292-4c7e-8d25-8834fcf3517a
ms.reviewer: mattsha
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: aaec456a5ff9864fedf5e95f317bc484ddfc4d82
ms.sourcegitcommit: fe7484e86ec8a109fa5f54fe9cceef8aac94bd9f
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80275075"
---
# <a name="windows-10-and-later-settings-to-protect-devices-using-intune"></a>Inställningar för Windows 10 (och senare) för att skydda delade enheter med Intune

Microsoft Intune innehåller många inställningar som skyddar dina enheter. Den här artikeln beskriver alla inställningar du kan aktivera och kon i Windows 10 och nyare enheter. Dessa inställningar skapas i en konfigurationsprofil för slutpunktsskydd i Intune för att kontrollera säkerheten, inklusive BitLocker och Microsoft Defender.  

Information om att konfigurera Microsoft Defender Antivirus finns i [Enhetsbegränsningar för Windows 10](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus).  

## <a name="before-you-begin"></a>Innan du börjar  

[Skapa en enhetskonfigurationsprofil för slutpunktsskydd](endpoint-protection-configure.md).  

Mer information om konfigurationstjänstproviders (CSP:er) finns i [Referens för konfigurationstjänstproviders](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference).  

## <a name="microsoft-defender-application-guard"></a>Microsoft Defender Application Guard  

När du använder Microsoft Edge Microsoft Defender Application Guard skyddas din miljö från webbplatser som inte är betrodda av din organisation. När användare besöker webbplatser som inte listas i din isolerade nätverksgräns, öppnas webbplatserna i en virtuell webbläsarsession i Hyper-V. Betrodda webbplatser definieras av en nätverksgräns som konfigureras i enhetskonfigurationen.  

Application Guard är endast tillgängligt för Windows 10-enheter (64-bitars). Med den här profilen installeras en Win32-komponent för att aktivera Application Guard.  

- **Application Guard**  
  **Standard**: Inte konfigurerat  
   CSP:n Application Guard: [Settings/AllowWindowsDefenderApplicationGuard](https://docs.microsoft.com/windows/client-management/mdm/windowsdefenderapplicationguard-csp#allowwindowsdefenderapplicationguard)  

  - **Aktivera för Edge** – aktiverar den här funktionen, som öppnar ej betrodda webbplatser i en virtualiserad Hyper-V-webbläsarcontainer.  
  - **Inte konfigurerat** – alla webbplatser (betrodda och ej betrodda) kan öppnas på enheten.  

- **Funktionssätt för Urklipp**  
  **Standard**: Inte konfigurerat  
   CSP:n Application Guard: [Settings/ClipboardSettings](https://go.microsoft.com/fwlink/?linkid=872351)  

  Välj vilka åtgärder för kopiera och klistra in som tillåts mellan den lokala datorn och den virtuella Application Guard-webbläsaren.  
  - **Inte konfigurerat**  
  - **Tillåt endast kopiera och klistra in från dator till webbläsare**  
  - **Tillåt endast kopiera och klistra in från webbläsare till dator**  
  - **Tillåt kopiera och klistra in mellan dator och webbläsare**  
  - **Blockera kopiera och klistra in mellan dator och webbläsare**  

- **Innehåll i Urklipp**  
  Den här inställningen är bara tillgänglig när *Funktionssätt för Urklipp* har någon av de *tillåtande* inställningarna.  
  **Standard**: Inte konfigurerat  
  CSP:n Application Guard: [Settings/ClipboardFileType](https://docs.microsoft.com/windows/client-management/mdm/windowsdefenderapplicationguard-csp#clipboardfiletype)  

  Välj det urklippsinnehåll som ska tillåtas.  
  - **Inte konfigurerat**  
  - **Text**  
  - **Bilder**  
  - **Text och bilder**  

- **Externt innehåll på företagswebbplatser**  
  **Standard**: Inte konfigurerat  
  CSP:n Application Guard: [Settings/BlockNonEnterpriseContent](https://go.microsoft.com/fwlink/?linkid=872352)  

  - **Blockera** – blockera inläsning av innehåll från webbplatser som inte är godkända.  
  - **Inte konfigurerad** – icke-företagswebbplatser kan öppnas på enheten.  
 
- **Skriv ut från virtuell webbläsare**  
  **Standard**: Inte konfigurerat  
  CSP:n Application Guard: [Settings/PrintingSettings](https://go.microsoft.com/fwlink/?linkid=872354)  

  - **Tillåt** – tillåter utskrift av valt innehåll från den virtuella webbläsaren.  
  - **Inte konfigurerat** Inaktivera alla utskriftsfunktioner.  

  När du *tillåter* utskrift kan du konfigurera följande inställning:
  - **Utskriftstyper** Välj ett eller flera av följande alternativ:  
    - PDF  
    - XPS  
    - Lokala skrivare
    - Nätverksskrivare  

- **Samla in loggar**  
  **Standard**: Inte konfigurerat  
  CSP:n Application Guard: [Audit/AuditApplicationGuard](https://go.microsoft.com/fwlink/?linkid=872418)  

  - **Tillåt** – samla in loggar för händelser som inträffar i en Application Guard-webbläsarsession.  
  - **Inte konfigurerad** – samlar inte in några loggar inom webbläsarsessionen.  

- **Behåll användargenererade webbläsardata**  
  **Standard**: Inte konfigurerat  
  CSP:n Application Guard: [Settings/AllowPersistence](https://go.microsoft.com/fwlink/?linkid=872419)  

  - **Tillåt** – spara användardata (t.ex. lösenord, favoriter och cookies) som skapas under en virtuell Application Guard-webbläsarsession.  
  - **Inte konfigurerad** – ta bort filer och data som laddats ned av en användare när enheten startas om eller när användaren loggar ut.  

- **Grafikacceleration**  
 **Standard**: Inte konfigurerat  
  CSP:n Application Guard: [Settings/AllowVirtualGPU](https://go.microsoft.com/fwlink/?linkid=872420)  
      
  - **Aktivera** – läs in grafikintensiva webbplatser och video snabbare genom att få åtkomst till en virtuell grafikprocessor.  
  - **Inte konfigurerat** Använd enhetens processor till grafik. Använd inte den virtuella grafikprocessorn.  

- **Ladda ned filer till värdfilsystemet**  
  **Standard**: Inte konfigurerat  
  CSP:n Application Guard: [Settings/SaveFilesToHost](https://go.microsoft.com/fwlink/?linkid=872421)  

  - **Aktivera** – användare laddar ned filer från den virtuella webbläsaren till värdoperativsystemet.  
  - **Inte konfigurerad** – håller filerna lokala på enheten och laddar inte ned filer till värdfilsystemet.  

## <a name="microsoft-defender-firewall"></a>Microsoft Defender-brandväggen  
 
### <a name="global-settings"></a>Globala inställningar  

De här inställningarna avser alla nätverkstyper.  

- **File Transfer Protocol**  
  **Standard**: Inte konfigurerat  
   CSP:n Firewall: [MdmStore/Global/DisableStatefulFtp](https://go.microsoft.com/fwlink/?linkid=872536)  

  - **Blockera** – inaktivera tillståndskänslig FTP.  
  - **Inte konfigurerad** – brandväggen utför tillståndskänslig FTP-filtrering för att tillåta sekundära anslutningar.  

- **Inaktiv tid för säkerhetsassociation före borttagning**  
  **Standard**: *Inte konfigurerat*  
   CSP:n Firewall: [MdmStore/Global/SaIdleTime](https://go.microsoft.com/fwlink/?linkid=872539)  

   Ange en inaktiv tid i sekunder efter vilken säkerhetsassociationer tas bort.   

- **Kodning av i förväg delad nyckel**  
  **Standard**: Inte konfigurerat  
   CSP:n Firewall: [MdmStore/Global/PresharedKeyEncoding](https://go.microsoft.com/fwlink/?linkid=872541)  

   - **Aktivera** – koda i förväg delade nycklar med UTF-8.  
   - **Inte konfigurerad** – koda i förväg delade nycklar med värdet i det lokala arkivet.  

- **IPsec-undantag**  
  **Standard**: *0 valda*  
   CSP:n Firewall: [MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

   Välj en eller flera av följande typer av trafik som ska undantas från IPsec:  
   - **Granne upptäcker koder av IPv6 ICMP-typ**  
   - **ICMP**  
   - **Router upptäcker koder av IPv6 ICMP-typ**  
   - **Både IPv4 och IPv6 DHCP-nätverkstrafik**  

- **Verifiering av listan över återkallade certifikat**  
  **Standard**: Inte konfigurerat  
  CSP:n Firewall: [MdmStore/Global/CRLcheck](https://go.microsoft.com/fwlink/?linkid=872548)  

  Välj hur enheten verifierar listan över återkallade certifikat. Alternativen är:  
  - **Inaktivera CRL-verifiering**  
  - **CRL-verifiering misslyckas enbart för återkallade certifikat**  
  - **CRL-verifiering misslyckas för alla påträffade fel**.  
 

- **Matcha autentiseringsuppsättningarna per nyckelmodul**  
  **Standard**: Inte konfigurerat  
  CSP:n Firewall: [MdmStore/Global/OpportunisticallyMatchAuthSetPerKM](https://go.microsoft.com/fwlink/?linkid=872550)  
  
  - **Aktivera** – nyckelmoduler MÅSTE endast ignorera de autentiseringspaket som de inte stödjer.  
  - **Inte konfigurerad** – nyckelmoduler MÅSTE ignorera hela autentiseringsuppsättningen om de inte har stöd för alla autentiseringspaket som anges i uppsättningen.  


- **Paketkö**  
  **Standard**: Inte konfigurerat  
  CSP:n Firewall: [MdmStore/Global/EnablePacketQueue](https://go.microsoft.com/fwlink/?linkid=872551)  

  Ange hur programvaruskalning på mottagarsidan aktiveras för den krypterade mottagningen och rensa flyttning av text framåt för scenariot med IPsec-tunnelgatewayen. Denna inställning bekräftar att paketordningen bevaras. Alternativen är:  
  - **Inte konfigurerat**  
  - **Inaktivera alla paketköer**  
  - **Ställ enbart inkommande krypterade paket i kö**  
  - **Köpaket efter det att dekrypteringen har genomförts enbart för vidarebefordran**  
  - **Konfigurera både inkommande och utgående paket**  

### <a name="network-settings"></a>Nätverksinställningar  

De här inställningarna visas bara en gång i den här artikeln, men alla gäller för de tre angivna nätverkstyperna:  
- **Domännätverk (arbetsyta)**  
- **Privat (synligt) nätverk**  
- **Offentligt (osynligt) nätverk**  

#### <a name="general-settings"></a>Allmänna inställningar  

- **Microsoft Defender-brandväggen**  
  **Standard**: Inte konfigurerat  
  CSP:n Firewall: [EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)  
  
  - **Aktivera** – aktivera brandväggen och avancerad säkerhet. 
  - **Inte konfigurerad** – tillåt all nätverkstrafik oavsett eventuella andra principinställningar.  

- **Dolt läge**  
  **Standard**: Inte konfigurerat  
  CSP:n Firewall: [DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)  
  - **Inte konfigurerat**  
  - **Blockera** – Brandväggen används inte i dolt läge. Om du blockerar dolt läge blockeras även **IPsec-skyddat paketundantag**.  
  - **Tillåt** – Brandväggen används i dolt läge, vilket hjälper till att förhindra svar på avsökningsförfrågningar.  

- **IPsec-skyddat paketetundantag med stealthläge**  
  **Standard**: Inte konfigurerat  
  CSP:n Firewall: [DisableStealthModeIpsecSecuredPacketExemption](https://go.microsoft.com/fwlink/?linkid=872560)  

  Det här alternativet ignoreras om *Dolt läge* har värdet *Blockera*.  

  - **Inte konfigurerat**  
  - **Blockera** – IPSec-skyddade paket undantas inte.  
  - **Tillåt** – Aktivera undantag. Brandväggens stealthläge får INTE förhindra värddatorn från att besvara oönskad nätverkstrafik som skyddas med IPsec.  

- **Avskärmad**  
  **Standard**: Inte konfigurerat  
  CSP:n Firewall: [Avskärmad](https://go.microsoft.com/fwlink/?linkid=872561)  
    - **Inte konfigurerat**  
    - **Blockera** – När Microsoft Defender-brandväggen är aktiverad och den här inställningen har värdet *Blockera* så blockeras all inkommande trafik oavsett eventuella andra policyinställningar. 
    - **Tillåt** – När den här inställningen har värdet *Tillåt* är den inaktiv och all inkommande trafik tillåts enligt andra policyinställningar.

- **Unicast-svar på multicast-sändningar**  
  **Standard**: Inte konfigurerat  
  CSP:n Firewall: [DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)  
  
  Normalt vill du inte ta emot unicast-svar på multicast- eller broadcast-meddelanden. Svaren kan indikera en DOS-attack (denial of service), eller en angripare som försöker avsöka en känd live-dator.  
  - **Inte konfigurerat**  
  - **Block** – Inaktivera Unicast-svar på multicast-sändningar.  
  - **Tillåt** – tillåt Unicast-svar på multicast-sändningar.  

- **Inkommande meddelanden**  
  **Standard**: Inte konfigurerat  
  CSP:n Firewall: [DisableInboundNotifications](https://go.microsoft.com/fwlink/?linkid=8725630)  

  - **Inte konfigurerat**  
  - **Blockera** – Dölj meddelanden till användarna när en app blockeras från att lyssna på en port.  
  - **Inte konfigurerad** – aktiverar inställningen och kan visa ett meddelande till användare när en app blockeras från att lyssna på en port.  

- **Standardåtgärd för inkommande anslutningar**  
  **Standard**: Inte konfigurerat  
  CSP:n Firewall: [DefaultOutboundAction](https://aka.ms/intune-firewall-outboundaction)  
  
  Konfigurera den standardåtgärd brandväggen ska utföra för utgående anslutningar. Den här inställningen gäller för Windows version 1809 och senare.  

  - **Inte konfigurerat**  
  - **Blockera** – Standardåtgärden för brandväggen utförs inte för utgående trafik om den inte uttryckligen har angetts att inte blockera.  
  - **Tillåt** – Standardåtgärden för brandväggen körs för alla utgående anslutningar.  

- **Standardåtgärd för inkommande anslutningar**  
  **Standard**: Inte konfigurerat  
  CSP:n Firewall: [DefaultInboundAction](https://go.microsoft.com/fwlink/?linkid=872564)  
 
  - **Inte konfigurerat**  
  - **Blockera** – brandväggens standardåtgärd körs inte på inkommande anslutningar.  
  - **Tillåt** – Standardåtgärden för brandväggen körs för alla inkommande anslutningar.  

#### <a name="rule-merging"></a>Sammanslagning av regler  

- **Microsoft Defender-brandväggsregler från det lokala arkivet**  
  **Standard**: Inte konfigurerat  
  CSP:n Firewall: [AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)  

  - **Inte konfigurerat**  
  - **Blockera inte** – reglerna för den auktoriserade programbrandväggen i det lokala arkivet ignoreras och framtvingas inte.  
  - **Tillåt** -
   Välj **Aktivera** för att tillämpa brandväggsregler i det lokala arkivet så att de känns igen och framtvingas.  

- **Globala Microsoft Defender-portalbrandväggen från det lokala arkivet**  
  **Standard**: Inte konfigurerat  
  CSP:n Firewall: [GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)  

  - **Inte konfigurerat**  
  - **Blockera** – Globala brandväggsregler för portar i det lokala arkivet ignoreras och framtvingas inte.  
  - **Aktivera** – tillämpa brandväggsregler på globala portar i det lokala arkivet så att de känns igen och framtvingas.  

- **Microsoft Defender-brandväggsregler från det lokala arkivet**  
  **Standard**: Inte konfigurerat  
  CSP:n Firewall: [AllowLocalPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872567)  

  - **Inte konfigurerat**  
  - **Blockera** – Brandväggsregler från det lokala arkivet ignoreras och framtvingas inte.
  - **Aktivera** – tillämpa brandväggsregler i det lokala arkivet så att de känns igen och framtvingas.  

- **IPSec-regler från det lokala arkivet**  
  **Standard**: Inte konfigurerat  
  CSP:n Firewall: [AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)  

  - **Inte konfigurerat**  
  - **Blockerad** – reglerna för anslutningssäkerhet från det lokala arkivet ignoreras och framtvingas inte, oavsett schemaversion eller version av regler för anslutningssäkerhet.  
  - **Tillåt** – tillämpa regler för anslutningssäkerhet från det lokala arkivet, oavsett schema eller version av regler för anslutningssäkerhet.  

### <a name="firewall-rules"></a>Brandväggsregler  

Du kan **lägga till** en eller flera egna brandväggsregler. Mer information finns i [Lägga till anpassade brandväggsregler för Windows 10-enheter](endpoint-protection-configure.md#add-custom-firewall-rules-for-windows-10-devices).  

För anpassade brandväggsregler finns följande alternativ:  

#### <a name="general-settings"></a>Allmänna inställningar:  

- **Namn**  
  **Standard**: *Inget namn*  

  Ange ett eget namn på din regel. Det här namnet visas i listan med regler så att du kan identifiera den.  

- **Beskrivning**  
  **Standard**: *Ingen beskrivning*  

  Ange en beskrivningen av regeln.  

- **Riktning**   
  **Standard**: Inte konfigurerat  
  CSP:n Firewall: [FirewallRules/*FirewallRuleName*/Direction](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#direction)  
  
  Ange om regeln ska gälla **Inkommande** eller **Utgående** trafik. När inställningen är **Inte konfigurerat** gäller regeln automatiskt för utgående trafik.  

- **Åtgärd**  
  **Standard**: Inte konfigurerat  
  CSP:n Firewall: [FirewallRules/*FirewallRuleName*/Action](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#action) och [FirewallRules/*FirewallRuleName*/Action/Type](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#type)  

  Välj mellan **Tillåt** och **Blockera**. När inställningen är **Inte konfigurerat** är standardregeln att tillåta trafik.  

- **Nätverkstyp**  
  **Standard**: 0 valda  
  CSP:n Firewall: [FirewallRules/*FirewallRuleName*/Profiles](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#profiles)  

  Välj upp till tre nätverkstyper som regeln ska tillhöra. Alternativen är **Domän**, **Privat** och **Offentligt**.  Om du inte väljer några nätverkstyper gäller regeln för alla tre nätverkstyper.  

#### <a name="application-settings"></a>Programinställningar  

- **Program**  
  **Standard**: Alla  

  Kontrollera anslutningar för en app eller ett program. Välj ett av följande alternativ och slutför sedan resten av konfigurationen:  
  - **Namn på paketfamilj** – ange namnet på en paketfamilj. Om du vill hitta namnet på paketfamiljen använder du PowerShell-kommandot **Get-AppxPackage**.   
    CSP:n Firewall: [FirewallRules/*FirewallRuleName*/App/PackageFamilyName](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#packagefamilyname)  
 
  - **Filsökväg** – du måste ange en filsökväg till en app på klientenheten. Det här kan vara en absolut eller relativ sökväg. Exempel:  C:\Windows\System\Notepad.exe eller %WINDIR%\Notepad.exe.  
    CSP:n Firewall: [FirewallRules/*FirewallRuleName*/App/FilePath](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#filepath)  

  - **Windows-tjänst** – ange kortnamnet för Windows-tjänsten om det är en tjänst och inte ett program som skickar eller tar emot trafik. Om du vill hitta tjänstens kortnamn använder du PowerShell-kommandot **Get-Service**.  
    CSP:n Firewall: [FirewallRules/*FirewallRuleName*/App/ServiceName](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#servicename)  

  - **Alla** – *ingen ytterligare konfiguration är tillgänglig*.  

#### <a name="ip-address-settings"></a>IP-adressinställningar  

Ange de lokala adresser och fjärradresser som regeln ska gälla.  

- **Lokala adresser**    
  **Standard**: Valfri adress  
  CSP:n Firewall: [FirewallRules/*FirewallRuleName*/LocalPortRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#localportranges)  

  Välj **Valfri adress** eller **Angiven adress**.  

  När du använder *Angiven adress* lägger du till en eller flera adresser som en kommaavgränsad lista med lokala adresser som omfattas av regeln. Giltiga token är:  
  - Använd en asterisk ”*” för *valfri* lokal adress. Om du använder en asterisk måste det vara den enda token du använder.  
  - Om du vill ange ett undernät använder du antingen nätmasken eller nätverkets prefix. Om du varken anger en nätmask eller ett nätverksprefix används standardvärdet 255.255.255.255 nätmask.  
  - En giltig IPv6-adress.  
  - Ett IPv4-adressintervall i formatet ”startadress-slutadress” utan blanksteg.  
  - Ett IPv6-adressintervall i formatet ”startadress-slutadress” utan blanksteg.  

- **Fjärradresser**  
  **Standard**: Valfri adress  
  CSP:n Firewall: [FirewallRules/*FirewallRuleName*/RemoteAddressRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#remoteaddressranges)  
 
  Välj **Valfri adress** eller **Angiven adress**.  

  När du använder *Angiven adress* lägger du till en eller flera adresser som en kommaavgränsad lista med fjärradresser som omfattas av regeln. Tokens är inte skiftlägeskänsliga. Giltiga token är:  
  - Använd en asterisk ”*” för *valfri* fjärradress. Om du använder en asterisk måste det vara den enda token du använder.  
  - "Defaultgateway"  
  - "DHCP"  
  - "DNS"  
  - ”WINS”  
  - "Intranet" (stöds i Windows-version 1809 och senare)  
  - "RmtIntranet" (stöds i Windows-version 1809 och senare)  
  - "Internet" (stöds i Windows-version 1809 och senare)  
  - "Ply2Renders" (stöds i Windows-version 1809 och senare)  
  - "LocalSubnet" avser valfri lokal adress i det lokala undernätet.  
  - Om du vill ange ett undernät använder du antingen nätmasken eller nätverkets prefix. Om du varken anger en nätmask eller ett nätverksprefix används standardvärdet 255.255.255.255 nätmask.  
  - En giltig IPv6-adress.  
  - Ett IPv4-adressintervall i formatet ”startadress-slutadress” utan blanksteg.  
  - Ett IPv6-adressintervall i formatet ”startadress-slutadress” utan blanksteg.  

#### <a name="port-and-protocol-settings"></a>Inställningar för portar och protokoll  
Ange de lokala portar och fjärrportar som regeln ska gälla.  

- **Protokoll**  
  **Standard**: Alla  
  CSP:n Firewall: [FirewallRules/*FirewallRuleName*/Protocol](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#protocol)  
  Välj bland följande och fyll i de konfigurationer som krävs:  
  - **Alla** – ingen ytterligare konfiguration är tillgänglig.  
  - **TCP** – konfigurera lokala portar och fjärrportar. För båda alternativen kan du välja Alla portar eller Angivna portar. Ange de angivna portarna i en kommaavgränsad lista.  
    - **Lokala portar** – CSP:n Firewall: [FirewallRules/*FirewallRuleName*/LocalPortRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#localportranges)  
    - **Fjärrportar** – CSP:n Firewall: [FirewallRules/*FirewallRuleName*/RemotePortRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#remoteportranges)  
  - **UDP** – konfigurera lokala portar och fjärrportar. För båda alternativen kan du välja Alla portar eller Angivna portar. Ange de angivna portarna i en kommaavgränsad lista.  
    - **Lokala portar** – CSP:n Firewall: [FirewallRules/*FirewallRuleName*/LocalPortRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#localportranges)  
    - **Fjärrportar** – CSP:n Firewall: [FirewallRules/*FirewallRuleName*/RemotePortRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#remoteportranges)  
  - **Anpassat** – ange ett eget **protokollnummer** från 0 till 255.  

#### <a name="advanced-configuration"></a>Avancerad konfiguration  
- **Gränssnittstyper**  
  **Standard**: 0 valda  
  CSP:n Firewall: [FirewallRules/*FirewallRuleName*/InterfaceTypes](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#interfacetypes)  

  Välj bland följande alternativ:  
  - **Fjärråtkomst**  
  - **Trådlöst**  
  - **Lokalt nätverk**  

- **Tillåt endast anslutningar från de här användarna**  
  **Standard**: Alla användare *(används som standard när du inte anger någon lista)*  
  CSP:n Firewall: [FirewallRules/*FirewallRuleName*/LocalUserAuthorizationList](https://aka.ms/intunefirewallauthorizedusers)  

  Ange en lista med behöriga lokala användare för den här regeln. Du kan inte ange någon lista med behöriga användare om den här regeln gäller för en Windows-tjänst.  


## <a name="microsoft-defender-smartscreen-settings"></a>Inställningar för Microsoft Defender SmartScreen  
 
Microsoft Edge måste vara installerat på enheten.  

- **SmartScreen för appar och filer**  
  **Standard**: Inte konfigurerat  
   CSP:n SmartScreen: [SmartScreen/EnableSmartScreenInShell](https://go.microsoft.com/fwlink/?linkid=872784)  

  - **Inte konfigurerat** – inaktiverar användningen av SmartScreen.  
  - **Aktivera** – aktiverar Windows SmartScreen för körning av filer och program som körs. SmartScreen är en molnbaserad komponent mot nätfiske och skadlig kod.  

- **Körning av overifierade filer**  
  **Standard**: Inte konfigurerat  
   CSP:n SmartScreen: [SmartScreen/PreventOverrideForFilesInShell](https://go.microsoft.com/fwlink/?linkid=872783)

  - **Inte konfigurerad** – inaktiverar den här funktionen och tillåter att slutanvändare kör filer som inte har verifierats.  
  - **Blockera** – hindrar slutanvändare från att köra filer som inte har verifierats av Windows SmartScreen.  

## <a name="windows-encryption"></a>Windows-kryptering  
 
### <a name="windows-settings"></a>Windows-inställningar  

- **Kryptera enheter**  
  **Standard**: Inte konfigurerat  
  CSP:n BitLocker: [RequireDeviceEncryption](https://go.microsoft.com/fwlink/?linkid=872523)  

  - **Kräv** – uppmana användare att aktivera enhetskryptering. Beroende på Windows-version och systemkonfiguration kan användare uppmanas att:  
    - Bekräfta att kryptering från en annan provider inte är aktiverat.  
    - Inaktivera Bitlocker-diskkryptering och aktivera sedan Bitlocker igen.  
  - **Inte konfigurerat**  
  
  Om Windows-kryptering aktiveras samtidigt som en annan krypteringsmetod är aktiv, kan enheten bli instabil.  

- **Kryptera minneskort (endast mobil)**  
  *Den här inställningen gäller endast mobila enheter med Windows 10.*  
  **Standard**: Inte konfigurerat  
  CSP:n BitLocker: [RequireStorageCardEncryption](https://go.microsoft.com/fwlink/?linkid=872524)  

  - **Kräv** för att kryptera flyttbara minneskort som används av enheten.  
  - **Inte konfigurerad** – kräv inte kryptering av minneskort och uppmana inte användaren att aktivera det.  

### <a name="bitlocker-base-settings"></a>Grundläggande BitLocker-inställningar  

Grundläggande inställningar är universella BitLocker-inställningar för alla typer av dataenheter. De här inställningarna styr vilka enhetskrypteringsåtgärder eller konfigurationsalternativ som användaren kan ändra för alla typer av dataenheter.  

- **Varning för annan hårddiskkryptering**  
  **Standard**: Inte konfigurerat  
  CSP:n BitLocker: [AllowWarningForOtherDiskEncryption](https://go.microsoft.com/fwlink/?linkid=872525)  

  - **Blockera** – inaktivera varningsmeddelandet om en annan tjänst för hårddiskkryptering finns på enheten.  
  - **Inte konfigurerat** – tillåt att varningen om annan diskkryptering visas.  

  > [!TIP]  
  > Om du vill installera BitLocker automatiskt i bakgrunden på en enhet som är ansluten till Azure AD och kör Windows 1809 eller senare måste den här inställningen ha värdet *Blockera*. Mer information finns i [Aktivera BitLocker i bakgrunden på enheter](../protect/encrypt-devices.md#silently-enable-bitlocker-on-devices).

  När värdet är *Blockera* kan du konfigurera följande inställning:  

  - **Låt standardanvändare aktivera kryptering under Azure AD-anslutning**  
    *Den här inställningen gäller bara för enheter anslutna till Azure Active Directory, `Warning for other disk encryption`.*  
    **Standard**: Inte konfigurerat  
    CSP:n BitLocker: [AllowStandardUserEncryption](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp#allowstandarduserencryption)

     - **Tillåt** – standardanvändare (inte administratörer) kan aktivera BitLocker-kryptering när de är inloggade.  
     - **Inte konfigurerad** – endast att administratörer får aktivera BitLocker-kryptering på enheten.  

  > [!TIP]  
  > Om du vill installera BitLocker automatiskt i bakgrunden på en enhet som är ansluten till Azure AD och kör Windows 1809 eller senare måste den här inställningen ha värdet *Tillåt*. Mer information finns i [Aktivera BitLocker i bakgrunden på enheter](../protect/encrypt-devices.md#silently-enable-bitlocker-on-devices).

- **Konfigurera krypteringsmetoder**  
  **Standard**: Inte konfigurerat  
  CSP:n BitLocker: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  

  - **Aktivera** – konfigurera krypteringsalgoritmer för operativsystem, data och flyttbara enheter.  
  - **Inte konfigurerad** – BitLocker använder 128-bitars XTS-AES som standardkrypteringsmetod eller använder den krypteringsmetod som anges av något installationsskript.  

  När värdet är *Aktivera* kan du konfigurera följande inställningar:  

  - **Kryptering för operativsystemenheter**  
    **Standard**: XTS-AES 128 bitar  
   
    Välj krypteringsmetod för operativsystemenheter. Vi rekommenderar att du använder XTS AES-algoritmen.  
    - **AES-CBC 128 bitar**  
    - **AES-CBC 256 bitar**  
    - **XTS-AES 128 bitar**  
    - **XTS-AES 256 bitar**  

  - **Kryptering för fasta dataenheter**  
    **Standard**: AES-CBC 128 bitar  
   
    Välj krypteringsmetod för fasta (inbyggda) dataenheter. Vi rekommenderar att du använder XTS AES-algoritmen.  
    - **AES-CBC 128 bitar**  
    - **AES-CBC 256 bitar**  
    - **XTS-AES 128 bitar**  
    - **XTS-AES 256 bitar**  

  - **Kryptering för flyttbara dataenheter**  
    **Standard**: AES-CBC 128 bitar  

    Välj krypteringsmetod för flyttbara dataenheter. Om den flyttbara enheten används med enheter som inte kör Windows 10 rekommenderar vi att du använder AES-CBC-algoritmen.  
    - **AES-CBC 128 bitar**  
    - **AES-CBC 256 bitar**  
    - **XTS-AES 128 bitar**  
    - **XTS-AES 256 bitar**  

### <a name="bitlocker-os-drive-settings"></a>BitLocker-inställningar för operativsystemenheten  

Dessa inställningar gäller specifikt för operativsystemets dataenheter.  

- **Ytterligare autentisering vid start**  
  **Standard**: Inte konfigurerat  
  CSP:n BitLocker: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)  

  - **Kräv** – konfigurera autentiseringskraven för datorstart, inklusive användning av Trusted Platform Module (TPM).  
  - **Inte konfigurerat** – konfigurera endast grundläggande alternativ på enheter med en TPM.  

  När värdet är *Kräv* kan du konfigurera följande inställningar:  

  - **BitLocker med icke-kompatibelt TPM-chip**  
    **Standard**: Inte konfigurerat  

    - **Blockera** – inaktivera användning av BitLocker när en enhet inte har ett kompatibelt TPM-chip.  
    - **Inte konfigurerad** – användare kan använda BitLocker utan ett kompatibelt TPM-chip. BitLocker kan kräva ett lösenord eller en startnyckel.  

  - **Kompatibel TPM-start**  
    **Standard**: Tillåt betrodd plattformsmodul  

    Ställ in om betrodd plattformsmodul ska tillåtas, krävas eller inte tillåtas.  

    - **Tillåt betrodd plattformsmodul**  
    - **Tillåt inte TPM**  
    - **Kräv betrodd plattformsmodul**  

  - **Kompatibel PIN-kod för TPM-start**  
    **Standard**: Tillåt start-PIN med betrodd plattformsmodul  

    Välj att tillåta, inte tillåta eller kräva användning av en PIN-kod för start med TPM-chippet. För att aktivera en PIN-kod för start krävs interaktion från slutanvändaren.  

    - **Tillåt start-PIN med betrodd plattformsmodul**  
    - **Tillåt inte start-PIN med betrodd plattformsmodul**  
    - **Kräv start-PIN med betrodd plattformsmodul**

    > [!TIP]
    > Om du vill installera BitLocker automatiskt i bakgrunden på en enhet som är ansluten till Azure AD och kör Windows 1809 eller senare måste den här inställningen ha värdet *Kräv start-PIN med betrodd plattformsmodul*. Mer information finns i [Aktivera BitLocker i bakgrunden på enheter](../protect/encrypt-devices.md#silently-enable-bitlocker-on-devices).

  - **Kompatibel nyckel för TPM-start**  
    **Standard**: Tillåt startnyckel med betrodd plattformsmodul  

    Välj att tillåta, inte tillåta eller kräva användning av en nyckel för start med TPM-chippet. För att aktivera en startnyckel krävs interaktion från slutanvändaren.  

    - **Tillåt startnyckel med betrodd plattformsmodul**  
    - **Tillåt inte startnyckel med betrodd plattformsmodul**  
    - **Kräv startnyckel med betrodd plattformsmodul**  

    > [!TIP]
    > Om du vill installera BitLocker automatiskt i bakgrunden på en enhet som är ansluten till Azure AD och kör Windows 1809 eller senare måste den här inställningen ha värdet *Kräv startnyckel med betrodd plattformsmodul*. Mer information finns i [Aktivera BitLocker i bakgrunden på enheter](../protect/encrypt-devices.md#silently-enable-bitlocker-on-devices).

  - **Kompatibel nyckel och PIN-kod för TPM-start**  
    **Standard**: Tillåt startnyckel och PIN-kod med betrodd plattformsmodul  

    Välj att tillåta, inte tillåta eller kräva användning av en nyckel och PIN-kod för start med TPM-chippet. För att aktivera en startnyckel och en PIN-kod krävs interaktion från slutanvändaren.  
    - **Tillåt startnyckel och PIN-kod med betrodd plattformsmodul**  
    - **Tillåt inte startnyckel och PIN-kod med betrodd plattformsmodul**  
    - **Kräv startnyckel och PIN-kod med betrodd plattformsmodul**   

    > [!TIP]  
    > Om du vill installera BitLocker automatiskt i bakgrunden på en enhet som är ansluten till Azure AD och kör Windows 1809 eller senare måste den här inställningen ha värdet *Kräv startnyckel och PIN-kod med betrodd plattformsmodul*. Mer information finns i [Aktivera BitLocker i bakgrunden på enheter](../protect/encrypt-devices.md#silently-enable-bitlocker-on-devices).

- **Minimilängd för PIN-kod**  
    **Standard**: Inte konfigurerat  
    CSP:n BitLocker: [SystemDrivesMinimumPINLength](https://go.microsoft.com/fwlink/?linkid=872528)   

    - **Aktivera** – konfigurera en minsta längd för start-PIN-koden för TPM.  
    - **Inte konfigurerad** – användare kan konfigurera en PIN-kod för start med valfri längd mellan 6 och 20 siffror.  

  När värdet är *Aktivera* kan du konfigurera följande inställning:  

  - **Minsta tecken**  
    **Standard**: *Inte konfigurerat* CSP:n BitLocker: [SystemDrivesMinimumPINLength](https://go.microsoft.com/fwlink/?linkid=872528)  

    Ange antalet tecken som krävs för PIN-koden från, **4**-**20**.  

- **Återställning av operativsystemenhet**  
  **Standard**: Inte konfigurerat   
  CSP:n BitLocker: [SystemDrivesRecoveryOptions](https://go.microsoft.com/fwlink/?linkid=872529)  

  - **Aktivera** – ange hur BitLocker-skyddade operativsystemenheter återställs när nödvändig startinformation saknas.  
  - **Inte konfigurerad** – standardåterställningsalternativen för BitLocker-återställning stöds. Som standard tillåts en DRA, återställningsalternativen väljs av användaren, inklusive återställningslösenordet och återställningsnyckeln och återställningsinformation säkerhetskopieras inte till AD DS.  

  När värdet är *Aktivera* kan du konfigurera följande inställningar:  

  - **Certifikatbaserad dataåterställningsagent**  
    **Standard**: Inte konfigurerat  
     
    - **Blockera** – spärra användningen av dataåterställningsagenter på operativsystemsenheter som skyddas med BitLocker.  
    - **Inte konfigurerat** – tillåt att dataåterställningsagenter används på operativsystemenheter som skyddas med BitLocker.  

  - **Återställningslösenord skapat av användare**  
    **Standard**: Tillåt 48-siffrigt återställningslösenord  

    Välj om användarna får, måste eller inte får generera ett 48-siffrigt återställningslösenord.  
    - **Tillåt 48-siffrigt återställningslösenord**  
    - **Tillåt inte 48-siffrigt återställningslösenord**  
    - **Kräv 48-siffrigt återställningslösenord**  

  - **Återställningsnyckel skapad av användare**  
    **Standard**: Tillåt 256-bitars återställningsnyckel  

    Välj om användarna får, måste eller inte får skapa en 256-bitars återställningsnyckel.  
    - **Tillåt 256-bitars återställningsnyckel**  
    - **Tillåt inte 256-bitars återställningsnyckel**  
    - **Kräv 256-bitars återställningsnyckel**  

  - **Återställningsalternativ i BitLocker-installationsguiden**  
    **Standard**: Inte konfigurerat  

    - **Blockera** – användarna kan inte se och ändra återställningsalternativen. När inställningen är 
    - **Inte konfigurerad** – användarna kan se och ändra återställningsalternativ när de aktiverar BitLocker. 
 
  - **Spara BitLocker-återställningsinformation i Azure Active Directory**  
    **Standard**: Inte konfigurerat  

    - **Aktivera** – lagra BitLocker-återställningsinformationen i Azure Active Directory (AAD).  
    - **Inte konfigurerat** – information om BitLocker-återställning lagras inte i AAD.  

  - **BitLocker-återställningsinformation lagras i Azure Active Directory**  
    **Standard**: Säkerhetskopiera återställningslösenord och nyckelpaket  

    Konfigurera vilka delar av BitLocker-återställningsinformation som lagras i Azure AD. Välj mellan:  
    - **Säkerhetskopiera återställningslösenord och nyckelpaket**  
    - **Säkerhetskopiera endast återställningslösenord**  

  - **Klientbaserad rotering av återställningslösenord**  
    **Standard**: Nyckelrotering har aktiverats för Azure AD-anslutna enheter  
    CSP:n BitLocker: [ConfigureRecoveryPasswordRotation](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp)  
    
    Med den här inställningen påbörjas en klientbaserad rotering av återställningslösenord efter en återställning av operativsystemenhet (antingen med bootmgr eller WinRE).  

    - Inte konfigurerat  
    - Nyckelrotering har inaktiverats  
    - Nyckelrotering har aktiverats för Azure AD-anslutna enheter  
    - Nyckelrotering har aktiverats för Azure AD- och hybridanslutna enheter  

  - **Lagra återställningsinformation i Azure Active Directory innan du aktiverar BitLocker**  
    **Standard**: Inte konfigurerat  
 
     Hindra att användare aktiverar BitLocker om inte datorn lyckas säkerhetskopiera BitLocker-återställningsinformationen till Azure Active Directory.  

    - **Kräv** – hindra användare från att aktivera BitLocker såvida inte BitLocker-återställningsinformation har lagrats i Azure AD.  
    - **Inte konfigurerad** – användare kan aktiverar BitLocker även om återställningsinformation inte har lagrats i Azure AD.  

- **Återställningsmeddelande och webbadress i förstartsmiljö**  
  **Standard**: Inte konfigurerat  
  CSP:n BitLocker: [SystemDrivesRecoveryMessage](https://go.microsoft.com/fwlink/?linkid=872530)  

  - **Aktivera** – konfigurera meddelandet och webbadressen som visas på återställningsskärmen innan start.  
  - **Inte konfigurerad** – inaktivera den här funktionen.  
  
  När värdet är *Aktivera* kan du konfigurera följande inställning:  
  - **Återställningsmeddelande i förstartsmiljö**  
    **Standard**: Använd standardvärde för återställningsmeddelande och webbadress   
 
    Konfigurera hur återställningsmeddelande i förstartsmiljö visas för användarna. Välj mellan:  
    - **Använd standardvärde för återställningsmeddelande och webbadress**  
    - **Använd tomt återställningsmeddelande och webbadress**  
    - **Använd anpassat återställningsmeddelande**  
    - **Använd anpassad återställningswebbadress**  

### <a name="bitlocker-fixed-data-drive-settings"></a>BitLocker-inställningar för fasta dataenheter  

De här inställningarna gäller specifikt fasta dataenheter.  

- **Skrivåtkomst till fast dataenhet som inte skyddas av BitLocker**  
  **Standard**: Inte konfigurerat  
  CSP:n BitLocker: [FixedDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872534)  

  - **Blockera** – ge skrivskyddad åtkomst till dataenheter som inte är BitLocker-skyddade.  
  - **Inte konfigurerat** – standardmässig läs- och skrivåtkomst till dataenheter som inte är krypterade.  

- **Återställning av fast enhet**  
  **Standard**: Inte konfigurerat  
  CSP:n BitLocker: [FixedDrivesRecoveryOptions](https://go.microsoft.com/fwlink/?linkid=872538)  

  - **Aktivera** – ange hur BitLocker-skyddade fasta enheter återställs när nödvändig startinformation saknas.  
  - **Inte konfigurerad** – inaktivera den här funktionen.  

  När värdet är *Aktivera* kan du konfigurera följande inställningar:  

  - **Dataåterställningsagent**  
    **Standard**: Inte konfigurerat  
 
    - **Blockera** – förhindra användning av dataåterställningsagent med principredigeraren för BitLocker-skyddade fasta enheter. 
    - **Inte konfigurerad** – tillåter användning av dataåterställningsagenter med BitLocker-skyddade fasta enheter.  

  - **Återställningslösenord skapat av användare**  
    **Standard**: Tillåt 48-siffrigt återställningslösenord  

    Välj om användarna får, måste eller inte får generera ett 48-siffrigt återställningslösenord.  
    - **Tillåt 48-siffrigt återställningslösenord**  
    - **Tillåt inte 48-siffrigt återställningslösenord**  
    - **Kräv 48-siffrigt återställningslösenord**  

  - **Återställningsnyckel skapad av användare**  
    **Standard**: Tillåt 256-bitars återställningsnyckel

    Välj om användarna får, måste eller inte får skapa en 256-bitars återställningsnyckel.
    - **Tillåt 256-bitars återställningsnyckel**  
    - **Tillåt inte 256-bitars återställningsnyckel**  
    - **Kräv 256-bitars återställningsnyckel**  

  - **Återställningsalternativ i BitLocker-installationsguiden**  
    **Standard**: Inte konfigurerat  

    - **Blockera** – användarna kan inte se och ändra återställningsalternativen. När inställningen är 
    - **Inte konfigurerad** – användarna kan se och ändra återställningsalternativ när de aktiverar BitLocker.
 
  - **Spara BitLocker-återställningsinformation i Azure Active Directory**  
    **Standard**: Inte konfigurerat  

    - **Aktivera** – lagra BitLocker-återställningsinformationen i Azure Active Directory (AAD).  
    - **Inte konfigurerat** – information om BitLocker-återställning lagras inte i AAD.

  - **BitLocker-återställningsinformation lagras i Azure Active Directory**  
    **Standard**: Säkerhetskopiera återställningslösenord och nyckelpaket  

    Konfigurera vilka delar av BitLocker-återställningsinformation som lagras i Azure AD. Välj mellan:  
    - **Säkerhetskopiera återställningslösenord och nyckelpaket**  
    - **Säkerhetskopiera endast återställningslösenord**  

  - **Klientbaserad rotering av återställningslösenord**  
    **Standard**: Nyckelrotering har aktiverats för Azure AD-anslutna enheter  
    CSP:n BitLocker: [ConfigureRecoveryPasswordRotation](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp)  
    
    Med den här inställningen påbörjas en klientbaserad rotering av återställningslösenord efter en återställning av operativsystemenhet (antingen med bootmgr eller WinRE).  

    - Inte konfigurerat  
    - Nyckelrotering har inaktiverats  
    - Nyckelrotering har aktiverats för Azure AD-anslutna enheter  
    - Nyckelrotering har aktiverats för Azure AD- och hybridanslutna enheter  

  - **Lagra återställningsinformation i Azure Active Directory innan du aktiverar BitLocker**  
    **Standard**: Inte konfigurerat  
 
    Hindra att användare aktiverar BitLocker om inte datorn lyckas säkerhetskopiera BitLocker-återställningsinformationen till Azure Active Directory.  

    - **Kräv** – hindra användare från att aktivera BitLocker såvida inte BitLocker-återställningsinformation har lagrats i Azure AD.  
    - **Inte konfigurerad** – användare kan aktiverar BitLocker även om återställningsinformation inte har lagrats i Azure AD.  

### <a name="bitlocker-removable-data-drive-settings"></a>BitLocker-inställningar för flyttbara dataenheter  

De här inställningarna gäller specifikt flyttbara dataenheter.  

- **Skrivåtkomst till flyttbar dataenhet som inte skyddas av BitLocker**  
  **Standard**: Inte konfigurerat  
  CSP:n BitLocker: [RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)  

  - **Blockera** – ge skrivskyddad åtkomst till dataenheter som inte är BitLocker-skyddade.  
  - **Inte konfigurerat** – standardmässig läs- och skrivåtkomst till dataenheter som inte är krypterade.  

  När värdet är *Aktivera* kan du konfigurera följande inställning:  

  - **Skrivåtkomst till enheter som har ställts in i en annan organisation**  
    **Standard**: Inte konfigurerat  

    - **Blockera** – blockerar skrivbehörighet för enheter som har konfigurerats i en annan organisation.  
    - **Inte konfigurerat** – neka skrivåtkomst.  
 
## <a name="microsoft-defender-exploit-guard"></a>Microsoft Defender Exploit Guard  

Använd [exploateringsskydd](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/exploit-protection) till att hantera och minska attackytan för appar som medarbetarna använder.  

### <a name="attack-surface-reduction"></a>Minska attackytan  

Reglerna för minskning av attackytan förhindrar beteenden som ofta används till att infektera datorer i skadlig kod.  

#### <a name="attack-surface-reduction-rules"></a>Regler för att minska attackytan  

- **Flagga stöld av inloggningsuppgifter från Windows Local Security Authority Subsystem**  
  **Standard**: Inte konfigurerat  
  Regel: [Blockera stöld av autentiseringsuppgifter från det lokala säkerhetsundersystemet i Windows (lsass.exe)](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-credential-stealing-from-the-windows-local-security-authority-subsystem)

  Hjälp till att förhindra åtgärder och appar som normalt används av skadlig kod som söker sårbarheter för att angripa datorer.  

  - **Inte konfigurerat**  
  - **Aktivera** Flagga stöld av inloggningsuppgifter från Windows Local Security Authority Subsystem (lsass.exe).  
  - **Endast granskning**  

- **Skapande av process från Adobe Reader (beta)**  
  **Standard**: Inte konfigurerat  
  Regel: [Blockera Adobe Reader från att skapa underordnade processer](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-adobe-reader-from-creating-child-processes)  

  - **Inte konfigurerat**  
  - **Aktivera** – blockera underordnade processer som skapas från Adobe Reader.  
  - **Endast granskning**  

#### <a name="rules-to-prevent-office-macro-threats"></a>Regler för att förhindra Office-makrohot  

Blockera Office-appar från att vidta följande åtgärder:  

- **Office-appar som infogar i andra processer (inga undantag)**  
  **Standard**: Inte konfigurerat  
  Regel: [Blockera Office-program från att infoga kod i andra processer](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-office-applications-from-injecting-code-into-other-processes)  

  - **Inte konfigurerat**  
  - **Blockera** – blockera Office-appar från att infoga kod i andra processer.  
  - **Endast granskning**  

- **Office-appar/-makron som skapar körbart innehåll**  
  **Standard**: Inte konfigurerat  
  Regel: [Blockera Office-program från att skapa körbart innehåll](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-office-applications-from-creating-executable-content)  

  - **Inte konfigurerat**  
  - **Blockera** – blockera Office-appar och makron från att skapa körbart innehåll.  
  - **Endast granskning**  

- **Office-appar som startar underordnade processer**  
  **Standard**: Inte konfigurerat  
  Regel: [Blockera Office-program från att skapa underordnade processer](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-all-office-applications-from-creating-child-processes)  

  - **Inte konfigurerat**  
  - **Blockera** – blockera Office-appar från att starta underordnade processer.  
  - **Endast granskning**  
  
- **Win32-importer från Office-makrokod**  
  **Standard**: Inte konfigurerat  
  Regel: [Blockera Win32-API-anrop från Office-makron](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-win32-api-calls-from-office-macros)  

  - **Inte konfigurerat**  
  - **Blockera** – blockera Win32-importer från makrokod i Office.  
  - **Endast granskning**  
  
- **Skapande av processer från Office-kommunikationsprodukter**  
  **Standard**: Inte konfigurerat  
  Regel: [Blockera Office-kommunikationsprogram från att skapa underordnade processer](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-office-communication-application-from-creating-child-processes)  

  - **Inte konfigurerat**  
  - **Aktivera** – blockera skapande av underordnade processer från Office-kommunikationsappar.  
  - **Endast granskning**  

#### <a name="rules-to-prevent-script-threats"></a>Regler för att förhindra skripthot  

Blockera följande för att hjälpa till att förhindra skripthot:  

- **Dold js/vbs/ps/makrokod**  
  **Standard**: Inte konfigurerat  
  Regel: [Blockera körning av potentiellt dolda skript](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-execution-of-potentially-obfuscated-scripts)    

  - **Inte konfigurerat**  
  - **Blockera** – blockera all dold js/vbs/ps/makrokod.  
  - **Endast granskning**  

- **js/vbs kör nyttolaster som laddats ned från Internet (inga undantag)**  
  **Standard**: Inte konfigurerat  
  Regel: [Blockera JavaScript eller VBScript från att starta nedladdat körbart innehåll](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-javascript-or-vbscript-from-launching-downloaded-executable-content)  

  - **Inte konfigurerat**  
  - **Blockera** – blockera js/vbs från att köra nyttolaster som laddats ned från internet.  
  - **Endast granskning**  

- **Skapa process från PSExec- och WMI-kommandon**  
  **Standard**: Inte konfigurerat  
  Regel: [Blockera skapande av processer från PSExec- och WMI-kommandon](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-process-creations-originating-from-psexec-and-wmi-commands)  

  - **Inte konfigurerat**  
  - **Blockera** – blockera skapande av processer från PSExec- och WMI-kommandon.  
  
  - **Endast granskning**  

- **Ej betrodda och osignerade processer som körs via USB**  
  **Standard**: Inte konfigurerat  
  Regel: [Blockera obetrodda och osignerade processer som körs via USB](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-untrusted-and-unsigned-processes-that-run-from-usb)    

  - **Inte konfigurerat**  
  - **Blockera** – blockera obetrodda och osignerade processer som körs via USB.  
  - **Endast granskning**  
  
- **Körbara filer som inte uppfyller ett villkor för användningsmönster, ålder eller betrodd lista**  
  **Standard**: Inte konfigurerat  
  Regel: [Blockera körbara filer från att köras om de inte uppfyller ett villkor för användningsmönster, ålder eller betrodd lista](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-executable-files-from-running-unless-they-meet-a-prevalence-age-or-trusted-list-criterion)    

  - **Inte konfigurerat**  
  - **Blockera** – blockera körbara filer från att köras om de inte uppfyller ett villkor för användningsmönster, ålder eller betrodd lista.  
  - **Endast granskning**  

#### <a name="rules-to-prevent-email-threats"></a>Regler för att förhindra e-posthot  

Blockera följande för att hjälpa till att förhindra e-posthot:  

- **Körning av körbart innehåll (exe, dll, ps, js, vbs, osv.) som har tagits bort från e-post (webbaserad e-post/e-postklient) (inga undantag)**  
  **Standard**: Inte konfigurerat  
  Regel: [Blockera körbart innehåll från e-postklient och webbaserad e-post](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-executable-content-from-email-client-and-webmail)  

  - **Inte konfigurerat**  
  - **Blockera** – blockera körning av körbart innehåll (exe, dll, ps, js, vbs, osv.) som har tagits bort från e-post (webbaserad e-post/e-postklient).  
  - **Endast granskning**  

#### <a name="rules-to-protect-against-ransomware"></a>Regler för skydd mot utpressningstrojaner  

- **Avancerat skydd mot utpressningstrojaner**  
  Standard:  Inte konfigurerat  
  Regel: [Använd avancerat skydd mot utpressningstrojaner](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#use-advanced-protection-against-ransomware)  

  - **Inte konfigurerat**  
  - **Aktivera** – använd aggressivt skydd mot utpressningstrojan.  
  - **Endast granskning**  

#### <a name="attack-surface-reduction-exceptions"></a>Undantag för att minska attackytan

- **Filer och mappar som ska uteslutas från reglerna för att minska attackytan**  
  CSP:n Defender: [AttackSurfaceReductionOnlyExclusions](https://go.microsoft.com/fwlink/?linkid=872981)  

  - **Importera** en .csv-fil med filer och mappar som ska undantas från reglerna om minskning av attackytan.  
  - **Lägg till** lokala filer eller mappar manuellt.  

> [!IMPORTANT]  
> För att tillåta korrekt installation och körning av verksamhetsspecifika Win32-appar bör inställningar för program mot skadlig kod undanta följande kataloger från att genomsökas:  
> **På X64-klientdatorer**:  
> *C:\Program Files (x86)\Microsoft Intune Management Extension\Content*  
> *C:\windows\IMECache*  
>  
> **På X86-klientdatorer**:  
> *C:\Program Files\Microsoft Intune Management Extension\Content*  
> *C:\windows\IMECache*  

### <a name="controlled-folder-access"></a>Reglerad mappåtkomst  

Hjälp till att [skydda värdefulla data](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/controlled-folders) från skadliga appar och hot, till exempel utpressningstrojaner.  

- **Mappskydd**  
  **Standard**: Inte konfigurerat  
  CSP:n Defender: [EnableControlledFolderAccess](https://go.microsoft.com/fwlink/?linkid=872614)  

  Skydda filer och mappar från obehöriga ändringar av oönskade appar.  

  - **Inte konfigurerat**  
  - **Aktivera**  
  - **Endast granskning**  
  - **Blockera diskändring**  
  - **Granska diskändring**  

  När du väljer ett annat värde än *Inte konfigurerat* kan du konfigurera följande:  
  - **Lista med appar som har åtkomst till skyddade mappar**  
    CSP:n Defender: [ControlledFolderAccessAllowedApplications](https://go.microsoft.com/fwlink/?linkid=872616)  

    - **Importera** en .csv-fil med en applista.  
    - **Lägg till** appar i den här listan manuellt.  

  - **Lista med ytterligare mappar som behöver skyddas**  
    CSP:n Defender: [ControlledFolderAccessProtectedFolders](https://go.microsoft.com/fwlink/?linkid=872617)  

    - **Importera** en .csv-fil med en mapplista.  
    - **Lägg till** mappar i den här listan manuellt.  

### <a name="network-filtering"></a>Nätverksfiltrering  

Blockera utgående anslutningar från alla appar till IP-adresser eller domäner med lågt anseende. Nätverksfiltrering stöds både i gransknings- och blockeringsläge.  

- **Nätverksskydd**  
  **Standard**: Inte konfigurerat  
  CSP:n Defender: [EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=872618)  

  Avsikten med den här inställningen är att skydda slutanvändarna från appar med åtkomst till nätfiskebedrägerier, exploaterande webbplatser och skadligt innehåll på internet. Den hindrar även att webbläsare från tredje part ansluter till farliga webbplatser.  

  - **Inte konfigurerad** – inaktivera den här funktionen. Användare och appar blockeras inte från att ansluta till farliga domäner. Administratörer kan inte se den här aktiviteten i Microsoft Defender Security Center.  
  - **Aktivera** – aktivera nätverksskydd och blockerar användare och appar från att ansluta till farliga domäner. Administratörer kan inte se den här aktiviteten i Microsoft Defender Security Center.  
  - **Endast granskning** – användare och appar blockeras inte från att ansluta till farliga domäner. Administratörer kan inte se den här aktiviteten i Microsoft Defender Security Center.  

### <a name="exploit-protection"></a>Sårbarhetsskydd  

- **Ladda upp XML**  
  **Standard**: *Inte konfigurerat*  

  Om du vill använda [skydd mot sårbarheter](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) skapar du en XML-fil som innehåller de inställningar för system- och programminskning du vill använda. Det finns två metoder för att skapa XML-filen:  

  - *PowerShell* – använd en eller flera av *Get-ProcessMitigation-* , *Set-ProcessMitigation-* och *ConvertTo-ProcessMitigationPolicy* PowerShell-cmdlets. Cmdlets konfigurerar åtgärdsinställningar och exporterar en XML-representation av dem.  

  - *Gränssnittet för Microsoft Defender Säkerhetscenter* – i Microsoft Defender Säkerhetscenter klickar du på App- & webbläsarkontroll och bläddrar sedan längst ned på skärmen för att hitta Sårbarhetsskydd. Använd först flikarna Systeminställningar och Programinställningar för att konfigurera minskningsinställningar. Leta sedan reda på länken Exportera inställningar längst ned på skärmen för att exportera en XML-återgivning av dem.  

- **Användarredigering av gränssnittet för sårbarhetsskydd**  
  **Standard**: Inte konfigurerat  
  CSP:n ExploitGuard: [ExploitProtectionSettings](https://go.microsoft.com/fwlink/?linkid=872887)  


  - **Blockera** – ladda upp en XML-fil som gör att du kan konfigurera begränsningar för minne, kontrollflöden och policyer. Inställningarna i XML-filen kan användas för att blockera ett program från kryphål.  
  - **Inte konfigurerat** – ingen anpassad konfiguration används.  

## <a name="microsoft-defender-application-control"></a>Microsoft Defender Application Control  

Välj ytterligare appar som antingen behöver granskas av eller som kan vara betrodda att köras av Microsoft Defender Application Control. Windows-komponenter och alla appar från Windows Store är automatiskt betrodda att köras.  


- **Kodintegritetsprinciper för programkontroll**  
  **Standard**: Inte konfigurerat  
   CSP: [CSP:n AppLocker](https://go.microsoft.com/fwlink/?linkid=874543)  

  - **Framtvinga** – välj kodintegritetsprinciper för programkontroll för användarnas enheter.  
  
    När det är aktiverat kan programkontrollen endast inaktiveras genom att ändra läget från *Framtvinga* till *Endast granskning*. Om du ändrar läget från *Framtvinga* till *Inte konfigurerad* fortsätter programkontrollen att tillämpas på tilldelade enheter.  

  - **Inte konfigurerat** – ingen programkontroll läggs till på enheterna. Inställningar som lagts till tidigare fortsätter dock att tillämpas på tilldelade enheter. 
 
  - **Endast granskning** – program blockeras inte. Alla händelser loggas i de lokala klientloggarna.  

## <a name="microsoft-defender-credential-guard"></a>Microsoft Defender Credential Guard  

Microsoft Defender Credential Guard skyddar mot attacker för stöld av autentiseringsuppgifter. Den isolerar hemligheter så att endast privilegierad programvara kan komma åt dem.  

- **Credential Guard**  
  **Standard**: Inaktivera  
  [CSP:n DeviceGuard](https://go.microsoft.com/fwlink/?linkid=872424)  

  - **Inaktivera** – stänger av Credential Guard via fjärranslutning om det tidigare har slagits på med alternativet **Aktivera utan UEFI-lås**.  

  - **Aktivera med UEFI-lås** – Credential Guard kan inte inaktiveras fjärrstyrt med en registernyckel eller grupprincip.  

    > [!NOTE]
    > Om du använder den här inställningen och sedan vill inaktivera Credential Guard, måste du ange grupprincipen till **Inaktiverad**. Och avmarkera UEFI-konfigurationsinformationen fysiskt från varje dator. Så länge UEFI-konfigurationen finns kvar är Credential Guard aktiverat.  

  - **Aktivera utan UEFI-lås** – tillåter att Credential Guard inaktiveras fjärrstyrt med hjälp av grupprincipen. Enheterna som använder den här inställningen måste köra Windows 10 version 1511 eller senare.  

  När du *aktiverar* Credential Guard aktiveras även följande nödvändiga funktioner:  
  
  - **Virtualiseringsbaserad säkerhet** (VBS)  
    Aktiveras vid nästa omstart. Virtualiseringsbaserad säkerhet använder Windows Hypervisor för att ge stöd för säkerhetstjänster.  
  - **Säker start med direkt minnesåtkomst**  
    Aktiverar VBS med säker start och DMA-skydd (direkt minnesåtkomst). DMA-skydd kräver maskinvarustöd och aktiveras endast på enheter som är korrekt konfigurerade.  

## <a name="microsoft-defender-security-center"></a>Microsoft Defender Security Center  

Microsoft Defender Security Center fungerar som en separat app eller process från var och en av de enskilda funktionerna. Den visar aviseringar via Action Center. Den fungerar som en insamlare eller enskild plats för att visa status och köra konfiguration för var och en av funktionerna. Läs mer i dokumentationen till [Microsoft Defender](https://docs.microsoft.com/windows/threat-protection/windows-defender-security-center/windows-defender-security-center).  

### <a name="microsoft-defender-security-center-app-and-notifications"></a>Appen Microsoft Defender Säkerhetscenter och meddelanden  

Blockera slutanvändarens åtkomst till olika delar av appen Microsoft Defender Säkerhetscenter. Om ett avsnitt döljs blockeras även relaterade meddelanden.  

- **Skydd mot virus och hot**  
  **Standard**: Inte konfigurerat  
  CSP:n WindowsDefenderSecurityCenter: [DisableVirusUI](https://go.microsoft.com/fwlink/?linkid=873662)  

  Konfigurera om slutanvändarna ska kunna visa området för skydd mot virus och hot i Microsoft Defender Security Center. Om du döljer det här avsnittet blockeras även alla meddelanden som rör skydd mot virus och hot.  

  - **Inte konfigurerat**  
  - **Dölj**  

- **Skydd mot utpressningstrojaner**  
  **Standard**: Inte konfigurerat  
  CSP:n WindowsDefenderSecurityCenter: [HideRansomwareDataRecovery](https://go.microsoft.com/fwlink/?linkid=873664)  

  Konfigurera om slutanvändarna ska kunna visa området för skydd mot utpressningstrojaner i Microsoft Defender Security Center. Om du döljer det här avsnittet blockeras även alla meddelanden som rör skydd mot utpressningstrojaner.  

  - **Inte konfigurerat**  
  - **Dölj**  

- **Kontoskydd**  
  **Standard**: Inte konfigurerat  
  CSP:n WindowsDefenderSecurityCenter: [DisableAccountProtectionUI](https://go.microsoft.com/fwlink/?linkid=873666)  

  Konfigurera om slutanvändarna ska kunna visa området för kontoskydd i Microsoft Defender Security Center. Om du döljer det här avsnittet blockeras även alla meddelanden som rör kontoskydd.  

  - **Inte konfigurerat**  
  - **Dölj**  

- **Brandväggs- och nätverksskydd**  
  **Standard**: Inte konfigurerat  
  CSP:n WindowsDefenderSecurityCenter: [DisableNetworkUI](https://go.microsoft.com/fwlink/?linkid=873668)  

  Konfigurera om slutanvändarna ska kunna visa området för brandvägg och nätverksskydd i Microsoft Defender Security Center. Om du döljer det här avsnittet blockeras även alla meddelanden som rör brandvägg och nätverksskydd.  

  - **Inte konfigurerat**  
  - **Dölj**  

- **App- och webbläsarkontroll**  
  **Standard**: Inte konfigurerat  
  WindowsDefenderSecurityCenter CSP: [DisableAppBrowserUI](https://go.microsoft.com/fwlink/?linkid=873669)  

  Konfigurera om slutanvändarna ska kunna visa området för app- och webbläsarkontroll i Microsoft Defender Security Center. Om du döljer det här avsnittet blockeras även alla meddelanden som rör app- och webbläsarkontroll.  

  - **Inte konfigurerat**  
  - **Dölj**  

- **Maskinvaruskydd**  
  **Standard**: Inte konfigurerat  
  CSP:n WindowsDefenderSecurityCenter: [DisableDeviceSecurityUI](https://go.microsoft.com/fwlink/?linkid=873670)  

  Konfigurera om slutanvändarna ska kunna visa området för maskinvaruskydd i Microsoft Defender Security Center. Om du döljer det här avsnittet blockeras även alla meddelanden som rör maskinvaruskydd.  

  - **Inte konfigurerat**  
  - **Dölj**  

- **Enhetsprestanda och hälsa**  
  **Standard**: Inte konfigurerat  
  WindowsDefenderSecurityCenter CSP: [DisableHealthUI](https://go.microsoft.com/fwlink/?linkid=873671)  

  Konfigurera om slutanvändarna ska kunna visa området för enhetsprestanda och hälsotillstånd i Microsoft Defender Security Center. Om du döljer det här avsnittet blockeras även alla meddelanden som rör enhetsprestanda och hälsotillstånd.  
  
  - **Inte konfigurerat**  
  - **Dölj**  

- **Familjealternativ**  
  **Standard**: Inte konfigurerat  
  CSP:n WindowsDefenderSecurityCenter: [DisableFamilyUI](https://go.microsoft.com/fwlink/?linkid=873673)  

  Konfigurera om slutanvändarna ska kunna visa området med familjealternativ i Microsoft Defender Security Center. Om du döljer det här avsnittet blockeras även alla meddelanden som rör familjealternativ.  
  
  - **Inte konfigurerat**  
  - **Dölj**  

- **Aviseringar från områdena som visas i appen**  
  **Standard**: Inte konfigurerat  
  CSP:n WindowsDefenderSecurityCenter: [DisableNotifications](https://go.microsoft.com/fwlink/?linkid=873675)  

  Välj vilka meddelanden som ska visas för slutanvändare. Meddelanden som är mindre viktiga omfattar sammanfattningar av Microsoft Defender Antivirus-aktivitet, inklusive meddelanden när genomsökningar har slutförts. Alla andra meddelanden anses viktiga.  

  - **Inte konfigurerat**  
  - **Blockera icke-kritiska aviseringar**  
  - **Blockera alla meddelanden**  

- **Ikon för Windows Security Center i systemfältet**  
  **Standard**: Inte konfigurerat  

  Konfigurera visningen av kontrollen för meddelandefältet. Användaren måste logga ut och logga in eller starta om datorn för att den här inställningen ska börja gälla.  
  
  - **Inte konfigurerat**  
  - **Dölj**  

- **Knappen Rensa TPM**  
  **Standard**: Inte konfigurerat  

  Konfigurera visningen av knappen Rensa TPM.  
  
  - **Inte konfigurerat**  
  - **Inaktivera**  

- **Varning om uppdatering av inbyggd TPM-programvara**  
  **Standard**: Inte konfigurerat  
  
  Konfigurera visningen av uppdatering av inbyggd TPM-programvara när sårbar inbyggd programvara identifieras.  

  - **Inte konfigurerat**  
  - **Dölj**  

- **Manipulationsskydd**  
  **Standard**: Inte konfigurerat

  Aktivera eller inaktivera manipulationsskydd på enheter. Om du vill använda manipulationsskydd måste du [integrera Microsoft Defender Advanced Threat Protection med Intune](advanced-threat-protection.md) och ha [licenser för Enterprise Mobility + Security E5](../fundamentals/licenses.md).  
  - **Inte konfigurerat** – enhetsinställningarna ändras inte.
  - **Aktiverat** – manipulationsskyddet aktiveras och begränsningar tillämpas på enheterna.
  - **Inaktiverat** – manipulationsskyddet inaktiveras och inga begränsningar framtvingas.

### <a name="it-contact-information"></a>IT-kontaktuppgifter  

Ange IT-kontaktuppgifter som ska visas i appen Microsoft Defender Säkerhetscenter och i appmeddelanden.  

Du kan välja **Visa i app och i aviseringar**, **Visa endast i app**, **Visa endast i aviseringar** eller **Visa inte**. Ange **IT-organisationens namn** och minst ett av följande kontaktalternativ:  


- **IT-kontaktuppgifter**  
  **Standard**: Visa inte  
  CSP:n WindowsDefenderSecurityCenter: [EnableCustomizedToasts](https://go.microsoft.com/fwlink/?linkid=873676)  
  
  Konfigurera var IT-kontaktinformationen ska visas för slutanvändarna.  
  
  - **Visa i app och i meddelanden**  
  - **Visa bara i app**  
  - **Visa bara i meddelanden**  
  - **Visa inte**  

  När informationen visas kan du konfigurera följande inställningar:  

  - **IT-organisationsnamn**  
    **Standard**: *Inte konfigurerat*  
    CSP:n WindowsDefenderSecurityCenter: [CompanyName](https://go.microsoft.com/fwlink/?linkid=873677)  

  - **IT-avdelningens telefonnummer eller Skype-ID**  
    **Standard**: *Inte konfigurerat*  
    CSP:n WindowsDefenderSecurityCenter: [Phone](https://go.microsoft.com/fwlink/?linkid=873678) 

  - **IT-avdelningens e-postadress**  
    **Standard**: *Inte konfigurerat*  
    CSP:n WindowsDefenderSecurityCenter: [E-post](https://go.microsoft.com/fwlink/?linkid=873679)  

  - **URL till IT-supportwebbplatsen**  
    **Standard**: *Inte konfigurerat*  
    CSP:n WindowsDefenderSecurityCenter: [URL](https://go.microsoft.com/fwlink/?linkid=873680)  
 
## <a name="local-device-security-options"></a>Säkerhetsalternativ för lokal enhet  

Använd dessa alternativ för att konfigurera de lokala säkerhetsinställningarna på Windows 10-enheter.  

### <a name="accounts"></a>Konton  

- **Lägg till nya Microsoft-konton**  
  **Standard**: Inte konfigurerat  
  CSP:n LocalPoliciesSecurityOptions: [Accounts_BlockMicrosoftAccounts](https://go.microsoft.com/fwlink/?linkid=867916)  


  - **Blockera** – förhindra att användare lägger till nya Microsoft-konton på enheten.  
  - **Inte konfigurerat** – användare kan använda Microsoft-konton på enheten.  

- **Fjärrinloggning utan lösenord**  
  **Standard**: Inte konfigurerat  
  CSP:n LocalPoliciesSecurityOptions: [Accounts_LimitLocalAccountUseOfBlankPasswordsToConsoleLogonOnly](https://go.microsoft.com/fwlink/?linkid=867890)  


   - **Aktivera** – tillåter endast lokala konton med tomma lösenord att logga in med enhetens tangentbord.  
   - **Inte konfigurerad** – tillåter att lokala konton med tomma lösenord loggar in från andra platser än den fysiska enheten.  

#### <a name="admin"></a>Administratör  

- **Lokalt administratörskonto**  
  **Standard**: Inte konfigurerat  
  CSP:n LocalPoliciesSecurityOptions: [Accounts_LimitLocalAccountUseOfBlankPasswordsToConsoleLogonOnly](https://go.microsoft.com/fwlink/?linkid=867850)  


  - **Blockera** – förhindra användning av lokala administratörskonton.  
  - **Inte konfigurerat**  

- **Byt namn på administratörskonto**  
  **Standard**: *Inte konfigurerat*  
  CSP:n LocalPoliciesSecurityOptions: [Accounts_RenameAdministratorAccount](https://go.microsoft.com/fwlink/?linkid=867917)  
 

  Definiera att ett annat kontonamn ska associeras med säkerhetsidentifieraren (SID) för kontot ”Administratör”.  

 #### <a name="guest"></a>Gäst  

- **Gästkonto**  
  **Standard**: Inte konfigurerat  
  CSP:n LocalPoliciesSecurityOptions: [LocalPoliciesSecurityOptions](https://go.microsoft.com/fwlink/?linkid=867853)  

  - **Blockera** – förhindra användning av gästkonton.  
  - **Inte konfigurerat**  

- **Byt namn på gästkonto**  
  **Standard**: *Inte konfigurerat*  
  CSP:n LocalPoliciesSecurityOptions: [Accounts_RenameGuestAccount](https://go.microsoft.com/fwlink/?linkid=867918)  
  
  Definiera att ett annat kontonamn ska associeras med säkerhetsidentifieraren (SID) för kontot ”Gäst”.  

### <a name="devices"></a>Egenskaper  

- **Koppla bort enhet från dockningsstation utan inloggning**  
  **Standard**: Inte konfigurerat  
  CSP:n LocalPoliciesSecurityOptions: [Devices_AllowUndockWithoutHavingToLogon](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-devices-allowundockwithouthavingtologon)  

  
  - **Blockera** – användarna kan trycka på den fysiska utmatningsknappen på en dockad bärbar enhet för att på ett säkert sätt koppla bort enheten.  
  - **Inte konfigurerat** – användare måste logga in på enheten och få behörighet att koppla bort enheten från dockningsstation.  

- **Installera skrivardrivrutiner för delade skrivare**  
  **Standard**:  Inte konfigurerat  
  CSP:n LocalPoliciesSecurityOptions: [Devices_PreventUsersFromInstallingPrinterDriversWhenConnectingToSharedPrinters](https://go.microsoft.com/fwlink/?linkid=867921)  


  - **Aktiverat** – alla användare kan installera en skrivardrivrutin som en del av anslutningen till en delad skrivare.  
  - **Inte konfigurerad** – endast administratörer kan installera en skrivardrivrutin som en del av anslutningen till en delad skrivare.  

- **Begränsa CD-ROM-åtkomsten till lokala aktiva användare**  
  **Standard**:  Inte konfigurerat  
  CSP: [Devices_RestrictCDROMAccessToLocallyLoggedOnUserOnly](https://go.microsoft.com/fwlink/?linkid=867922)  


  - **Aktiverat** – endast den interaktivt inloggade användaren kan använda CD-ROM-media. Om den här principen är aktiverad och ingen är interaktivt inloggad används CD-ROM via nätverket.  
  - **Inte konfigurerat** – alla har åtkomst till CD-ROM-enheten.  

- **Formatera och mata ut flyttbar media**  
  **Standard**: Administratörer  
  CSP: [Devices_AllowedToFormatAndEjectRemovableMedia](https://go.microsoft.com/fwlink/?linkid=867920)  
 

  Definiera vem som får formatera och mata ut flyttbar NTFS-media:  
  - **Inte konfigurerat**  
  - **Administratörer**  
  - **Administratörer och privilegierade användare**  
  - **Administratörer och interaktiva användare**  

### <a name="interactive-logon"></a>Interaktiv inloggning  

- **Minuter av låsskärmsinaktivitet innan skärmsläckaren aktiveras**  
  **Standard**: *Inte konfigurerat*  
  CSP:n LocalPoliciesSecurityOptions: [InteractiveLogon_MachineInactivityLimit](https://go.microsoft.com/fwlink/?linkid=867891)  


  Ange högsta antal minuter av inaktivitet på det interaktiva skrivbordets inloggningsskärm tills skärmsläckaren startar. (**0** - **99999**)  

- **Kräv CTRL+ALT+DEL för att logga in**:  
  **Standard**: Inte konfigurerat  
  CSP:n LocalPoliciesSecurityOptions: [InteractiveLogon_DoNotRequireCTRLALTDEL](https://go.microsoft.com/fwlink/?linkid=867951)  


  - **Aktivera** – användare måste inte trycka på CTRL+ALT+DEL för att logga in.  
  - **Inte konfigurerad** – kräv att användarna trycker på CTRL+ALT+DEL innan de loggar in på Windows.  

- **Beteende vid borttagning av smartkort**  
  **Standard**: Lås arbetsstation   
  CSP:n LocalPoliciesSecurityOptions: [InteractiveLogon_SmartCardRemovalBehavior](https://go.microsoft.com/fwlink/?linkid=868437)  
    
  Avgör vad som händer när smartkortet för en inloggad användare tas bort från smartkortsläsaren. Alternativen är:  

  - **Låsa arbetsstationen** – arbetsstationen låses när smartkortet tas bort. Med det här alternativet kan användare lämna området, ta med sig smartkortet och fortfarande skydda sessionen.  
  - **Ingen åtgärd**  
  - **Framtvinga utloggning** – användaren loggas ut automatiskt när smartkortet tas bort.  
  - **Koppla från om Remote Desktop Services-session** – om smartkortet tas bort så kopplas sessionen från utan att användaren loggas ut. Med det här alternativet kan användaren sätta i smartkortet och fortsätta sessionen senare, eller vid en annan dator med smartkortsläsare, utan att behöva logga in igen. Om sessionen är lokal fungerar den här principen precis som Lås arbetsstationen.  

#### <a name="display"></a>Visning  

- **Användarinformation på låsskärmen**  
  **Standard**: Inte konfigurerat  
  CSP:n LocalPoliciesSecurityOptions: [InteractiveLogon_DisplayUserInformationWhenTheSessionIsLocked](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-interactivelogon-displayuserinformationwhenthesessionislocked)  

  Konfigurera användarinformation som visas när sessionen är låst. Om inställningen inte konfigureras visas användarens visningsnamn, domän och användarnamn.  

  - **Inte konfigurerat**  
  - **Användarens visningsnamn, domän och användarnamn**  
  - **Endast användarens visningsnamn**  
  - **Visa inte användarinformation**  

- **Dölj användarnamn vid inloggning**  
  **Standard**: Inte konfigurerat  
  CSP:n LocalPoliciesSecurityOptions: [InteractiveLogon_DoNotDisplayLastSignedIn](https://go.microsoft.com/fwlink/?linkid=868437)  
  
  
  - **Aktivera** – dölj användarnamnet.  
  - **Inte konfigurerat** – visa det senaste användarnamnet.  

- **Dölj användarnamn vid inloggning**
  **Standard**: Inte konfigurerat  
  CSP:n LocalPoliciesSecurityOptions: [InteractiveLogon_DoNotDisplayUsernameAtSignIn](https://go.microsoft.com/fwlink/?linkid=867959)  

  
  - **Aktivera** – dölj användarnamnet.  
  - **Inte konfigurerat** – visa det senaste användarnamnet.  

- **Meddelanderubrik vid inloggning**  
  **Standard**: *Inte konfigurerat*  
  CSP:n LocalPoliciesSecurityOptions: [InteractiveLogon_MessageTitleForUsersAttemptingToLogOn](https://go.microsoft.com/fwlink/?linkid=867964)  

  Ställ in meddelanderubrik för användare som loggar in.  

- **Meddelandetext vid inloggning**  
  **Standard**: *Inte konfigurerat*  
  CSP:n LocalPoliciesSecurityOptions: [InteractiveLogon_MessageTextForUsersAttemptingToLogOn](https://go.microsoft.com/fwlink/?linkid=867962)  

  Ställ in meddelandetext för användare som loggar in.  
  
### <a name="network-access-and-security"></a>Åtkomst till nätverket och säkerhet

- **Anonym åtkomst till namngivna pipes och resurser**  
  **Standard**: Inte konfigurerat  
  CSP:n LocalPoliciesSecurityOptions: [NetworkAccess_RestrictAnonymousAccessToNamedPipesAndShares](https://go.microsoft.com/fwlink/?linkid=868432)  

  - **Inte konfigurerat** – anonym åtkomst begränsas till resurs- och namngivna pipe-inställningar. Gäller för de inställningar som kan användas anonymt.  
  - **Blockera** – inaktivera policyn så att anonym åtkomst blir tillgänglig.  

- **Anonym uppräkning av SAM-konton**  
  **Standard**: Inte konfigurerat  
  CSP:n LocalPoliciesSecurityOptions: [NetworkAccess_DoNotAllowAnonymousEnumerationOfSAMAccounts](https://go.microsoft.com/fwlink/?linkid=868434)  
  
  - **Inte konfigurerat** – anonyma användare kan räkna upp SAM-konton.  
  - **Blockera** – förhindra anonym uppräkning av SAM-konton.  

- **Anonym uppräkning av SAM-konton och resurser**  
  **Standard**: Inte konfigurerat  
  CSP:n LocalPoliciesSecurityOptions: [NetworkAccess_DoNotAllowAnonymousEnumerationOfSamAccountsAndShares](https://go.microsoft.com/fwlink/?linkid=868435)  

  - **Inte konfigurerat** – anonyma användare kan räkna upp namn på domänkonton och nätverksresurser.  
  - **Blockera** – blockera anonym uppräkning av SAM-konton och resurser. 

- **LAN Manager-hashvärdet lagras vid ändring av lösenord**  
  **Standard**: Inte konfigurerat  
  CSP:n LocalPoliciesSecurityOptions: [NetworkSecurity_DoNotStoreLANManagerHashValueOnNextPasswordChange](https://go.microsoft.com/fwlink/?linkid=868431)  
   
  Avgör om hashvärdet för lösenord lagras nästa gång lösenordet ändras. 
  - **Inte konfigurerat** – hashvärdet lagras inte.  
  - **Blockera** – LAN Manager (LM) lagrar hashvärdet för det nya lösenordet.  

- **PKU2U-autentiseringsförfrågningar**  
  **Standard**: Inte konfigurerat  
  CSP:n LocalPoliciesSecurityOptions: [NetworkSecurity_AllowPKU2UAuthenticationRequests](https://go.microsoft.com/fwlink/?linkid=867892)  

  - **Inte konfigurerat** – tillåt PU2U-förfrågningar.  
  - **Blockera** – blockera PKU2U-autentiseringsförfrågningar till den här enheten.  

- **Begränsa RPC-fjärranslutningar till SAM**  
  **Standard**: Inte konfigurerat  
  CSP:n LocalPoliciesSecurityOptions: [NetworkAccess_RestrictClientsAllowedToMakeRemoteCallsToSAM](https://go.microsoft.com/fwlink/?linkid=867893)  
  
  - **Inte konfigurerat** – använd standardsäkerhetsbeskrivningen, som kan tillåta användare och grupper att göra RPC-fjärranrop till hanteringen av mjukvarutillgångar.
  - **Tillåt** – neka användare och grupper från att göra RPC-fjärranrop till hanteringen av mjukvarutillgångar, som lagrar användarkonton och lösenord. Med **Tillåt** kan du även ändra SDDL-standardsträngen (Security Descriptor Definition Language) så att den explicit tillåter eller nekar användare och grupper att göra de här fjärranropen.  

    - **Säkerhetsbeskrivning**  
      **Standard**: *Inte konfigurerat*  
    
- **Minsta sessionssäkerhet för NTLM SSP-baserade klienter**  
  **Standard**: Inga  
  CSP:n LocalPoliciesSecurityOptions: [NetworkSecurity_MinimumSessionSecurityForNTLMSSPBasedClients](https://aka.ms/policy-csp-localpoliciessecurityoptions-networksecurity-minimumsessionsecurityforntlmsspbasedclients)  
  
  Den här säkerhetsinställningen gör att en server kan kräva förhandling av 128-bitarskryptering och/eller NTLMv2-sessionssäkerhet.  

  - **Inga**  
  - **Kräv NTLMv2-sessionssäkerhet**  
  - **Kräv 128-bitarskryptering**  
  - **NTLMv2 och 128-bitarskryptering**  
 
- **Minsta sessionssäkerhet för NTLM SSP-baserade servrar**  
  **Standard**: Inga  
  CSP:n LocalPoliciesSecurityOptions: [NetworkSecurity_MinimumSessionSecurityForNTLMSSPBasedServers](https://aka.ms/policy-csp-localpoliciessecurityoptions-networksecurity-minimumsessionsecurityforntlmsspbasedservers)  

  Den här säkerhetsinställningen avgör vilket autentiseringsprotokoll för anrop/svar som används för nätverksinloggningar.  

  - **Inga**  
  - **Kräv NTLMv2-sessionssäkerhet**  
  - **Kräv 128-bitarskryptering**  
  - **NTLMv2 och 128-bitarskryptering**  

- **Autentiseringsnivå för LAN Manager**  
  **Standard**: LM och NTLM  
  CSP:n LocalPoliciesSecurityOptions: [NetworkSecurity_LANManagerAuthenticationLevel](https://aka.ms/policy-csp-localpoliciessecurityoptions-lanmanagerauthenticationlevel)  


  - **LM och NTLM**  
  - **LM, NTLM och NTLMv2**  
  - **NTLM**  
  - **NTLMv2**  
  - **NTLMv2 men inte LM**  
  - **NTLMv2 men inte LM eller NTLM**  
  
- **Osäkra gästinloggningar**  
  **Standard**: Inte konfigurerat  
  CSP:n LanmanWorkstation: [LanmanWorkstation](https://aka.ms/policy-csp-lanmanworkstation-enableinsecureguestlogons)  

  Om du aktiverar den här inställningen avvisar SMB-klienten osäkra gästinloggningar.  

  - **Inte konfigurerat**  
  - **Blockera** – SMB-klienten avvisar osäkra gästinloggningar.  

### <a name="recovery-console-and-shutdown"></a>Återställningskonsol och avstängning  

- **Rensa virtuell växlingsfil när du stänger**  
  **Standard**: Inte konfigurerat  
   CSP:n LocalPoliciesSecurityOptions: [Shutdown_ClearVirtualMemoryPageFile](https://go.microsoft.com/fwlink/?linkid=867914)  


  - **Aktivera** – rensa den virtuella växlingsfilen när enheten stängs av.  
  - **Inte konfigurerad** – rensar inte det virtuella minnet.  

- **Stäng av utan inloggning**  
  **Standard**: Inte konfigurerat  
  CSP:n LocalPoliciesSecurityOptions: [Shutdown_AllowSystemToBeShutDownWithoutHavingToLogOn](https://go.microsoft.com/fwlink/?linkid=867912)  

  
  - **Blockera** – dölj avstängningsalternativet på Windows-inloggningsskärmen. Användarna måste logga in på enheten och sedan stänga av den.  
  - **Inte konfigurerad** – användare kan stänga av enheten från Windows-inloggningsskärmen.  

### <a name="user-account-control"></a>User account control  

- **UIA-integritet utan säker plats**  
  **Standard**: Inte konfigurerat  
  CSP:n LocalPoliciesSecurityOptions: [UserAccountControl_OnlyElevateUIAccessApplicationsThatAreInstalledInSecureLocations](https://go.microsoft.com/fwlink/?linkid=867897)  
  
  - **Blockera** – appar på skyddade platser i filsystemet körs endast med UIAccess-integritet.  
  - **Inte konfigurerad** – appar kan köras med UIAccess-integritet även om apparna inte finns på en säker plats i filsystemet.  

- **Virtualisera skrivfel för filer och register till platser per användare**  
  **Standard**: Inte konfigurerat  
  CSP:n LocalPoliciesSecurityOptions: [UserAccountControl_VirtualizeFileAndRegistryWriteFailuresToPerUserLocations](https://go.microsoft.com/fwlink/?linkid=867900)  

  - **Aktiverat** – program som skriver data till skyddade platser nekas.  
  - **Ej konfigurerad** – programskrivfel omdirigeras under körning till definierade användarplatser för filsystemet och registret.  

- **Utöka endast behörighet för körbara filer som har signerats och verifierats**  
  **Standard**: Inte konfigurerat  
  CSP:n LocalPoliciesSecurityOptions: [UserAccountControl_OnlyElevateUIAccessApplicationsThatAreInstalledInSecureLocations](https://go.microsoft.com/fwlink/?linkid=867965)  

  - **Aktiverat** – framtvinga verifiering av PKI-certifikatsökväg för en körbar fil innan den kan köras.  
  - **Inte konfigurerad** – framtvinga inte verifiering av PKI-certifikatsökväg innan en körbar fil kan köras.  

#### <a name="uia-elevation-prompt-behavior"></a>Beteende vid UIA:s fråga om utökad behörighet  

- **Fråga om utökade privilegier för administratörer**  
  **Standard**: Fråga efter medgivande för binärfiler som inte är Windows  
  CSP:n LocalPoliciesSecurityOptions: [UserAccountControl_BehaviorOfTheElevationPromptForAdministrators](https://go.microsoft.com/fwlink/?linkid=867895)  

  Definiera funktionssätt för fråga om utökade privilegier för administratörer i Läge för administratörstillåtelse.  

  - **Inte konfigurerat**  
  - **Utöka privilegier utan att fråga**  
  - **Fråga efter autentiseringsuppgifter på det skyddade skrivbordet**  
  - **Fråga efter autentiseringsuppgifter**  
  - **Fråga efter medgivande**  
  - **Fråga efter medgivande för binära filer som inte tillhör Windows**  


- **Fråga om utökade privilegier för standardanvändare**  
  **Standard**: Fråga efter autentiseringsuppgifter  
  CSP:n LocalPoliciesSecurityOptions: [UserAccountControl_BehaviorOfTheElevationPromptForStandardUsers](https://go.microsoft.com/fwlink/?linkid=867896)  

  Definiera funktionssätt för fråga om utökade privilegier för standardanvändare.  

  - **Inte konfigurerat**  
  - **Neka förfrågningar om höjd behörighet automatiskt**  
  - **Fråga efter autentiseringsuppgifter på det skyddade skrivbordet**  
  - **Fråga efter autentiseringsuppgifter**  

- **Vidarebefordra frågor om utökade privilegier till användarens interaktiva skrivbord**  
  **Standard**: Inte konfigurerat  
  CSP:n LocalPoliciesSecurityOptions: [UserAccountControl_SwitchToTheSecureDesktopWhenPromptingForElevation](https://go.microsoft.com/fwlink/?linkid=867899)  


  - **Aktiverat** – alla frågor om utökade privilegier går till den interaktiva användarens skrivbord i stället för det skyddade skrivbordet. Eventuella principinställningar för beteende vid fråga om utökad behörighet för administratörer och standardanvändare används.  
  - **Inte konfigurerad** – framtvingar att alla förfrågningar om höjd behörighet går till det skyddade skrivbordet oavsett eventuella principinställningar för beteende vid fråga om utökad behörighet för administratörer och standardanvändare.

- **Fråga om utökad behörighet för appinstallationer**  
  **Standard**: Inte konfigurerat  
  CSP:n LocalPoliciesSecurityOptions: [UserAccountControl_DetectApplicationInstallationsAndPromptForElevation](https://go.microsoft.com/fwlink/?linkid=867901)  

   - **Aktiverat** – Programinstallationspaket identifieras inte eller inga frågor om utökade privilegier visas.
   - **Inte konfigurerad** – användaren uppmanas att ange ett administrativt användarnamn och lösenord när ett paket för programinstallation kräver utökade behörigheter.

- **Fråga från UIA om utökad behörighet utan skyddat skrivbord**  
  **Standard**: Inte konfigurerat  
  CSP:n LocalPoliciesSecurityOptions: [UserAccountControl_AllowUIAccessApplicationsToPromptForElevation](https://go.microsoft.com/fwlink/?linkid=867894)  

- **Aktivera** – tillåter UIAccess-appar att fråga om utökade privilegier utan att använda skyddat skrivbord.  
- **Inte konfigurerat** – frågor om utökade privilegier går till ett skyddat skrivbord.  

#### <a name="admin-approval-mode"></a>Använd läge för administratörstillåtelse  

- **Läge för administratörstillåtelse för inbyggd administratör**  
  **Standard**: Inte konfigurerat  
  CSP:n LocalPoliciesSecurityOptions: [UserAccountControl_UseAdminApprovalMode](https://go.microsoft.com/fwlink/?linkid=867902)  

  - **Aktiverad** – tillåter att det inbyggda administratörskontot använder läget för administratörstillåtelse. Alla åtgärder som kräver rättighetsökning uppmanar användaren att godkänna åtgärden.  
  - **Inte konfigurerad** – kör alla appar med fullständiga administratörsrättigheter.  

- **Kör alla administratörer i läge för administratörstillåtelse**  
  **Standard**: Inte konfigurerat  
  CSP:n LocalPoliciesSecurityOptions: [UserAccountControl_RunAllAdministratorsInAdminApprovalMode](https://go.microsoft.com/fwlink/?linkid=867898)  


  - **Aktiverat** – aktivera läget för administratörstillåtelse.  
  - **Inte konfigurerat** – läge för administratörstillåtelse och alla relaterade UAC-principinställningar.  

### <a name="microsoft-network-client"></a>Microsoft-nätverksklient  

- **Signera kommunikationer digitalt (om servern tillåter)**  
  **Standard**: Inte konfigurerat  
  CSP:n LocalPoliciesSecurityOptions: [MicrosoftNetworkClient_DigitallySignCommunicationsIfServerAgrees](https://go.microsoft.com/fwlink/?linkid=868423)  

  Avgör om SMB-klienten förhandlar signering av SMB-paket.  
  - **Blockera** – SMB-klienten förhandlar aldrig SMB-paketsignering.
  - **Inte konfigurerat** – Microsoft-nätverksklienten ber servern att utföra SMB-paketsignering när sessionen konfigureras. Om paketsignering är aktiverad på servern så förhandlas paketsignering.  

- **Skicka okrypterade lösenord till SMB-servrar från tredje part**  
  **Standard**: Inte konfigurerat  
  CSP:n LocalPoliciesSecurityOptions: [MicrosoftNetworkClient_SendUnencryptedPasswordToThirdPartySMBServers](https://go.microsoft.com/fwlink/?linkid=868426)  


  - **Blockera** – SMB-omdirigeraren (Server Message Block) kan skicka lösenord i klartext till Microsoft SMB-servrar som inte har stöd för kryptering av lösenord under autentiseringen.  
  - **Inte konfigurerat** – blockera sändning av lösenord i klartext. Lösenorden är krypterade.  

- **Signera kommunikation digitalt (alltid)**  
  **Standard**: Inte konfigurerat  
  CSP:n LocalPoliciesSecurityOptions: [MicrosoftNetworkClient_DigitallySignCommunicationsAlways](https://go.microsoft.com/fwlink/?linkid=868425)  


  - **Aktivera** – Microsoft-nätverksservern kommunicerar inte med en Microsoft-nätverksklient såvida inte klienten godkänner signering av SMB-paket.  
  - **Inte konfigurerat** – SMB-paketsignering förhandlas mellan klienten och servern.  

### <a name="microsoft-network-server"></a>Microsoft-nätverksserver  
  
- **Signera kommunikation digitalt (om klienten tillåter)**  
  **Standard**: Inte konfigurerat  
  CSP: [MicrosoftNetworkServer_DigitallySignCommunicationsIfClientAgrees](https://go.microsoft.com/fwlink/?linkid=868429)  

  - **Aktiverad** – Microsoft-nätverksservern förhandlar SMB-paketsignering såsom begärs av klienten. D.v.s. om paketsignering är aktiverat på servern, förhandlas paketsignering.  
  - **Inte konfigurerat** – SMB-klienten förhandlar aldrig SMB-paketsignering.  

- **Signera kommunikation digitalt (alltid)**  
  **Standard**: Inte konfigurerat  
  CSP: [MicrosoftNetworkServer_DigitallySignCommunicationsAlways](https://go.microsoft.com/fwlink/?linkid=868428)  

  - **Aktivera** – Microsoft-nätverksservern kommunicerar inte med en Microsoft-nätverksklient såvida inte klienten godkänner signering av SMB-paket.  
  - **Inte konfigurerat** – SMB-paketsignering förhandlas mellan klienten och servern.  

## <a name="xbox-services"></a>Xbox-tjänster

- **Uppgiften Spara Xbox-spel**  
  **Standard**: Inte konfigurerat  
  CSP: [TaskScheduler/EnableXboxGameSaveTask](https://go.microsoft.com/fwlink/?linkid=875480)  
   
  Den här inställningen avgör om speluppgiften Spara i Xbox-spel är aktiverad eller inte.  
  - **Aktiverad**
  - **Inte konfigurerat**

- **Hanteringstjänst för Xbox-tillbehör**  
  **Standard**: Manuell  
  CSP: [SystemServices/ConfigureXboxAccessoryManagementServiceStartupMode](https://go.microsoft.com/fwlink/?linkid=875481)  

  Den här inställningen avgör starttypen för tillbehörshanteringstjänsten.  
  - **Manuell**
  - **Automatiskt**
  - **Inaktiverad**

- **Tjänsten Xbox Live Auth Manager**  
  **Standard**: Manuell  
  CSP: [SystemServices/ConfigureXboxLiveAuthManagerServiceStartupMode](https://go.microsoft.com/fwlink/?linkid=875482)  
 
  Den här inställningen avgör starttypen för Live Auth Manager-tjänsten.  
  - **Manuell**
  - **Automatiskt**
  - **Inaktiverad**
 
- **Tjänsten Xbox Live Game Save**  
  **Standard**: Manuell  
  CSP: [SystemServices/ConfigureXboxLiveGameSaveServiceStartupMode](https://go.microsoft.com/fwlink/?linkid=875483)  

  Den här inställningen avgör starttypen för Live Game Save-tjänsten.  
  - **Manuell**
  - **Automatiskt**
  - **Inaktiverad**

- **Tjänsten Xbox Live Networking**  
  **Standard**: Manuell  
  CSP: [SystemServices/ConfigureXboxLiveNetworkingServiceStartupMode](https://go.microsoft.com/fwlink/?linkid=875484)  

  Den här inställningen avgör starttypen för Networking-tjänsten.  
  - **Manuell**
  - **Automatiskt**
  - **Inaktiverad**

## <a name="next-steps"></a>Nästa steg

Profilen har skapats, men den gör inte något än. [Tilldela profilen](../configuration/device-profile-assign.md) och [övervaka dess status](../configuration/device-profile-monitor.md).  

Konfigurera inställningar för slutpunktsskydd på [macOS](endpoint-protection-macos.md)-enheter.  
