---
title: Inställningar för Intune Endpoint Security-brandvägg | Microsoft Docs
description: Principinställningar för Endpoint Security-brandvägg för Windows och macOS i Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: d90870a60ea292939926816bb74b5d285dc6a09f
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431611"
---
# <a name="firewall-policy-settings-for-endpoint-security-in-intune"></a>Inställningar för brandväggsprinciper för slutpunktssäkerhet i Intune

Visa de inställningar du kan konfigurera i profiler för policyn *Brandvägg* i noden Slutpunktssäkerhet i Intune inom ramen för [policyn Slutpunktssäkerhet](../protect/endpoint-security-policy.md).

Plattformar och profiler som stöds:

- **macOS**:
  - Profil: **macOS-brandvägg**

- **Windows 10 och senare**:
  - Profil: **Microsoft Defender-brandväggen**

## <a name="macos-firewall-profile"></a>profil för macOS-brandvägg

### <a name="firewall"></a>Brandvägg

Följande inställningar konfigureras som [Endpoint Security-princip för macOS-brandväggar](../protect/endpoint-security-firewall-policy.md)

- **Aktivera brandvägg**

  - **Ej konfigurerat** (*standard*)
  - **Ja** – Aktivera brandväggen.
  
  När värdet är *Ja* kan du konfigurera följande inställningar.  

  - **Blockera alla inkommande anslutningar**

    - **Ej konfigurerat** (*standard*)
    - **Ja** – Blockera alla inkommande anslutningar utom anslutningar som behövs för grundläggande internettjänster, som DHCP, Bonjour och IPSec. Det här blockerar också alla delningstjänster.

  - **Aktivera dolt läge**

    - **Ej konfigurerat** (*standard*)
    - **Ja** – Förhindra att datorn svarar på avsökningsbegäranden. Datorn svarar fortfarande på inkommande begäranden för behöriga appar.

  - **Brandväggsappar** Expandera listrutan och välj sedan **Lägg till** och ange sedan appar och regler för inkommande anslutningar för appen.
    - **Tillåt inkommande anslutningar**
      - Inte konfigurerat
      - Blockera
      - Tillåt

    - **Paket-ID** – ID:t identifierar appen. Exempel: *com.apple.app*

## <a name="microsoft-defender-firewall-profile"></a>Microsoft Defender-brandväggsprofil

### <a name="microsoft-defender-firewall"></a>Microsoft Defender-brandväggen

Följande inställningar konfigureras som [slutpunktssäkerhetsprincip för Windows 10-brandväggar](../protect/endpoint-security-firewall-policy.md).

- **Inaktivera tillståndskänsligt filöverföringsprotokoll (FTP)**  
  CSP: [MdmStore/Global/DisableStatefulFtp](https://go.microsoft.com/fwlink/?linkid=872536)

  - **Inte konfigurerat** (*standard*) – Brandväggen använder FTP för att kontrollera och filtrera sekundära nätverksanslutningar, vilket kan göra att brandväggsreglerna ignoreras.
  - **Ja**
  
- **Antal sekunder som en säkerhetsassociation kan vara inaktiv innan den tas bort**  
  CSP: [MdmStore/Global/SaIdleTime](https://go.microsoft.com/fwlink/?linkid=872539)

  Ange en tid i sekunder mellan 300 och 3600 för hur länge säkerhetsassociationerna ska sparas efter det att nätverkstrafiken inte har visats.
  
  Om du inte anger något värde tar systemet bort en säkerhetsassociation när den har varit inaktiv i 300 sekunder.
  
- **Kodning för i förväg delad nyckel**  
  CSP: [MdmStore/Global/PresharedKeyEncoding](https://go.microsoft.com/fwlink/?linkid=872541)

  Om du inte kräver *UTF-8* kommer i förväg delade nycklar initialt att kodas med UTF-8. Efter det kan enhetsanvändare välja en annan kodningsmetod.

  - **Ej konfigurerat** (*standard*)
  - **Inga**
  - **UTF8**

- **Brandväggs- och IPsec-undantag tillåter grannidentifiering**  
  CSP: [MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - **Ej konfigurerat** (*standard*)
  - **Ja** – Brandväggs- och IPsec-undantag tillåter grannidentifiering.

- **Brandväggs- och IPsec-undantag tillåter ICMP**  
  CSP: [MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - **Ej konfigurerat** (*standard*)
  - **Ja** – Brandväggs- och IPsec-undantag tillåter ICMP.

- **Brandväggs- och IPsec-undantag tillåter routeridentifiering**  
  CSP: [MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - **Ej konfigurerat** (*standard*)
  - **Ja** – Brandväggs- och IPsec-undantag tillåter routeridentifiering.

- **Brandväggs- och IPsec-undantag tillåter DHCP**  
  CSP: [MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - **Ej konfigurerat** (*standard*)
  - **Ja** – Brandväggs- och IPsec-undantag tillåter DHCP

- **Kontroll av lista över återkallade certifikat**  
  CSP: [MdmStore/Global/CRLcheck](https://go.microsoft.com/fwlink/?linkid=872548)

   Ange hur kontroll av listan över återkallade certifikat ska aktiveras.
  - **Inte konfigurerad** (*standard*) – klientens standard är att inaktivera CRL-verifiering.
  - **Inga**
  - **Försök**
  - **Kräv**

- **Kräver att nyckelmoduler endast ska ignorera de autentiseringspaket som de inte stödjer**  
  CSP: [MdmStore/Global/OpportunisticallyMatchAuthSetPerKM](https://go.microsoft.com/fwlink/?linkid=872550)

  - **Ej konfigurerat** (*standard*)
  - **Ja** – Nyckelmoduler ignorerar autentiseringspaket som inte stöds.

- **Paketkö**  
  CSP: [MdmStore/Global/EnablePacketQueue](https://go.microsoft.com/fwlink/?linkid=872551)

  Ange hur skalning för programvara på mottagarsidan aktiveras för den krypterade mottagningen och rensa flyttning av text framåt för scenariot med IPsec-tunnelgatewayen. Detta säkerställer att paketordningen bevaras.
  - **Inte konfigurerat** (*standard*) – Paketköer skickas tillbaka till klientens standardvärde, vilket är inaktiverad.
  - **Inaktiverad**
  - **Kö inkommande**
  - **Kö utgående**
  - **Kö båda**

- **Aktivera Microsoft Defender-brandväggen för domännätverk**  
  CSP: [EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

  - **Inte konfigurerad** (*standard*) – Klienten återgår till standardvärdet, vilket är att aktivera brandväggen.
  - **Ja** – Microsoft Defender-brandväggen för nätverkstypen **domän** aktiveras och framtvingas.
  - **Nej** – Inaktivera brandväggen.

- **Aktivera Microsoft Defender-brandväggen för domännätverk**  
  CSP: [EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

  - **Inte konfigurerad** (*standard*) – Klienten återgår till standardvärdet, vilket är att aktivera brandväggen.
  - **Ja** – Microsoft Defender-brandväggen för nätverkstypen **privat** aktiveras och framtvingas.
  - **Nej** – Inaktivera brandväggen.

- **Aktivera Microsoft Defender-brandväggen för offentliga nätverk**  
  CSP: [EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

  - **Inte konfigurerad** (*standard*) – Klienten återgår till standardvärdet, vilket är att aktivera brandväggen.
  - **Ja** – Microsoft Defender-brandväggen för nätverkstypen **offentlig** aktiveras och framtvingas.
  - **Nej** – Inaktivera brandväggen.

<!-- Microsoft Defender Firewall rules added in 2005  -->

### <a name="microsoft-defender-firewall-rules"></a>Brandväggsregler för Microsoft Defender

*Den här profilen är i förhandsversion*.

Följande inställningar konfigureras som [slutpunktssäkerhetsprincip för Windows 10-brandväggar](../protect/endpoint-security-firewall-policy.md).

#### <a name="windows-firewall-rule"></a>Windows-brandväggsregel

- **Namn**  
  Ange ett eget namn på din regel. Det här namnet visas i listan med regler så att du kan identifiera den.

- **Beskrivning**  
  Ange en beskrivningen av regeln.

- **Riktning**  
  - **Inte konfigurerad** (*standard*) – den här regeln används som standard för utgående trafik.
  - **Ut** – Den här regeln tillämpas på utgående trafik.
  - **In** – Den här regeln tillämpas på ingående trafik.

- **Åtgärd**  
  - **Inte konfigurerad** (*standard*) – Regeln används som standard för att tillåta trafik.
  - **Blockerad** – Trafik blockeras i den *riktning* du har konfigurerat.
  - **Tillåten** – Trafik tillåts i den *riktning* du har konfigurerat.

- **Nätverkstyp**  
  Ange de nätverkstypen som regeln tillhör. Välj något av följande. Om du inte väljer något alternativ gäller regeln för alla nätverkstyper.
  - **Domän**
  - **Privat**
  - **Offentlig**
  - **Inte konfigurerat**

- **Paketserienamn**  
  [Get-AppxPackage](https://docs.microsoft.com/previous-versions//hh856044(v=technet.10))

  Du kan hämta paketserienamn genom att köra kommandot Get-AppxPackage från PowerShell.

- **Filsökväg**  
  CSP: [FirewallRules/FirewallRuleName/App/FilePath](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#filepath)

  Ange sökvägen till appen på klientenheten om du vill ange sökvägen till den. Till exempel: `C:\Windows\System\Notepad.exe` eller `%WINDIR%\Notepad.exe`

- **Tjänstnamn**  
  [FirewallRules/FirewallRuleName/App/ServiceName](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#servicename)

  Använd ett kort namn för Windows-tjänsten när en tjänst, inte ett program, skickar eller tar emot trafik. Korta tjänstnamn hämtar du genom att köra kommandot `Get-Service` från PowerShell.

- **Protokoll**  
  CSP: [FirewallRules/FirewallRuleName/Protocol](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#protocol)

  Ange protokollet för den här portregeln.
  - Med transportlagerprotokoll som *TCP (6)* och *UDP (17)* kan du ange portar eller portintervall.
  - För anpassade protokoll anger du ett tal mellan *0* och *255* som representerar IP-protokollet.
  - När inget anges använder regeln standardvärdet **Alla**.

- **Gränssnittstyper**  
  Ange de gränssnittstyper som regeln tillhör. Välj något av följande. Om du inte väljer något alternativ gäller regeln för alla gränssnittstyper:
  - **Fjärråtkomst**
  - **Trådlöst**
  - **Lokalt nätverk**
  - **Inte konfigurerat**

- **Behöriga användare**  
  [FirewallRules/FirewallRuleName/LocalUserAuthorizationList](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#localuserauthorizedlist)

  Ange en lista med behöriga lokala användare för den här regeln. Du kan inte ange någon lista med behöriga användare om *tjänstnamnet* i den här principen är inställd som en Windows-tjänst. Om ingen auktoriserad användare anges är standardvärdet *alla användare*.

- **Valfri lokal adress**  
  **Inte konfigurerad** (*standard*) – Använd inställningen *Intervall för lokal adress** för att konfigurera ett intervall med adresser som ska stödjas.
  - **Ja** – Stöd för alla lokala adresser och konfigurerar inget adressintervall.

- **Intervall för lokal adress**  
  CSP: [FirewallRules/FirewallRuleName/LocalAddressRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#localaddressranges)  

  Lägg till en eller flera adresser som en kommaavgränsad lista med lokala adresser som omfattas av regeln. Giltiga poster (token) innehåller följande alternativ:
  - **En asterisk** – En asterisk (\*) anger vilken lokal adress som helst. Om den finns måste asterisken vara den enda token som ingår.
  - **Ett undernät** – Ange undernät med nätmasken eller nätverkets prefix. Om du inte anger någon nätmask eller ett nätverksprefix används standardvärdet 255.255.255.255.
  - **En giltig IPv6-adress**
  - **Ett IPv4-adressintervall** – IPv4-intervall måste anges i formatet *startadress-slutadress* utan blanksteg, där startadressen är mindre än slutadressen.
  - **Ett IPv6-adressintervall** – IPv6-intervall måste anges i formatet *startadress-slutadress* utan blanksteg, där startadressen är mindre än slutadressen.

  När inget värde anges använder den här inställningen standardvärdet *Valfri adress*.

- **Valfri fjärradress**  
  **Inte konfigurerad** (*standard*) – Använd inställningen *Fjärradressintervall** för att konfigurera ett intervall med adresser som ska stödjas.
  - **Ja** – Stöder alla fjärradresser och konfigurerar inget adressintervall.

- **Fjärradressintervall**  
  CSP: [FirewallRules/FirewallRuleName/RemoteAddressRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#remoteaddressranges)  

  Lägg till en eller flera adresser som en kommaavgränsad lista med fjärradresser som omfattas av regeln. Giltiga poster (token) inkluderar följande och är inte skiftlägeskänsliga:
  - **En asterisk** – En asterisk (\*) anger vilken fjärradress som helst. Om den finns måste asterisken vara den enda token som ingår.
  - **Defaultgateway**
  - **DHCP**
  - **DNS**
  - **WINS**
  - **Intranet** – Stöds på enheter som kör Windows 1809 eller senare.
  - **RmtIntranet** – Stöds på enheter som kör Windows 1809 eller senare.
  - **Ply2Renders** – Stöds på enheter som kör Windows 1809 eller senare.
  - **LocalSubnet** – avser valfri lokal adress i det lokala undernätet.
  - **Ett undernät** – Ange undernät med nätmasken eller nätverkets prefix. Om du inte anger någon nätmask eller ett nätverksprefix används standardvärdet 255.255.255.255.
  - **En giltig IPv6-adress**
  - **Ett IPv4-adressintervall** – IPv4-intervall måste anges i formatet *startadress-slutadress* utan blanksteg, där startadressen är mindre än slutadressen.
  - **Ett IPv6-adressintervall** – IPv6-intervall måste anges i formatet *startadress-slutadress* utan blanksteg, där startadressen är mindre än slutadressen.

  När inget värde anges använder den här inställningen standardvärdet *Valfri adress*.

<!-- End of 2005 additions  -->

## <a name="next-steps"></a>Nästa steg

[Princip för slutpunktssäkerhet för brandväggar](../protect/endpoint-security-firewall-policy.md)
