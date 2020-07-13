---
title: Baslinjeinställningar för Intune-säkerhet för Microsoft Defender Avancerat skydd
titleSuffix: Microsoft Intune
description: Inställningar för säkerhetsbaslinjer som stöds av Intune för att hantera Microsoft Defender Avancerat skydd
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/06/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: laarrizz
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
zone_pivot_groups: atp-baseline-versions
ms.openlocfilehash: 8046318c55e2a9791f01fca4a5a54de3f1487782
ms.sourcegitcommit: b90d51f7ce09750e024b97baf6950a87902a727c
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/06/2020
ms.locfileid: "86022201"
---
<!-- Pivots in use: 
::: zone pivot="atp-april-2020"
::: zone-end

::: zone pivot="atp-march-2020"
::: zone-end

::: zone pivot="atp-march-2020,atp-april-2020"
::: zone-end
-->

# <a name="microsoft-defender-advanced-threat-protection-baseline-settings-for-intune"></a>Baslinjeinställningar för Intune för Microsoft Defender Avancerat skydd

Visa baslinjeinställningarna för Microsoft Defender Avancerat skydd som stöds av Microsoft Intune. Standardinställningarna för ATP-baslinjen (Advanced Threat Protection) representerar den rekommenderade konfigurationen för ATP och kanske inte överensstämmer med baslinjens standardvärden för andra säkerhetsbaslinjer.

::: zone pivot="atp-april-2020"

Informationen i den här artikeln gäller version 4 av Microsoft Defender ATP-baslinjen, som gavs ut den 21 april 2020. För att förstå vad som är nytt i den här versionen av baslinjen jämfört med tidigare versioner kan du använda aktiviteten [Jämför baslinjer](../protect/security-baselines.md#compare-baseline-versions) som är tillgänglig när du visar fönstret *Versioner* för den här baslinjen.

::: zone-end
::: zone pivot="atp-march-2020"

Informationen i den här artikeln gäller version 3 av Microsoft Defender Avancerat skydd-baslinjen, som gavs ut den 1 mars 2020. För att förstå vad som är nytt i den här versionen av baslinjen jämfört med tidigare versioner kan du använda aktiviteten [Jämför baslinjer](../protect/security-baselines.md#compare-baseline-versions) som är tillgänglig när du visar fönstret *Versioner* för den här baslinjen.

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"


Baslinjen för Microsoft Defender Advanced Threat Protection är tillgänglig när din miljö uppfyller förhandskraven för att använda [Microsoft Defender Advanced Threat Protection](advanced-threat-protection.md#prerequisites).

Baslinjen är optimerad för fysiska enheter och rekommenderas inte för användning på virtuella datorer (VM) eller VDI-slutpunkter. Vissa baslinjeinställningar kan påverka fjärranslutna interaktiva sessioner i virtualiserade miljöer. Mer information finns i [Öka efterlevnaden med säkerhetsbaslinjen i Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-machines-security-baseline) i Windows-dokumentationen.


## <a name="application-guard"></a>Application Guard

Mer information finns i [WindowsDefenderApplicationGuard CSP](https://docs.microsoft.com/windows/client-management/mdm/windowsdefenderapplicationguard-csp) i Windows-dokumentationen.  

När du använder Microsoft Edge Microsoft Defender Application Guard skyddas din miljö från webbplatser som inte är betrodda av din organisation. När användare besöker webbplatser som inte listas i din isolerade nätverksgräns, öppnas webbplatserna i en virtuell webbläsarsession i Hyper-V. Betrodda webbplatser definieras av en nätverksgräns.  

- **Aktivera Application Guard för Edge (alternativ)**  
  CSP: [Settings/AllowWindowsDefenderApplicationGuard](https://go.microsoft.com/fwlink/?linkid=872350)
  
  - **Aktiverat för Edge** (*standard*) – Application Guard öppnar icke-godkända webbplatser i en Hyper-V-virtualiserad webbläsarcontainer.
  - **Inte konfigurerat** – Alla webbplatser (betrodda och ej betrodda) öppnas på enheten och inte i en virtualiserad container.  
  
  När du har angett *Aktivera för Edge* kan du konfigurera *Blockera externt innehåll från webbplatser som inte godkänts av företaget* och *Funktionssätt för Urklipp*.

  - **Blockera externt innehåll från webbplatser som inte godkänts av företaget**  
    CSP: [Settings/BlockNonEnterpriseContent](https://go.microsoft.com/fwlink/?linkid=872352)

    - **Ja** (*standard*) – Blockera inläsning av innehåll från webbplatser som inte är godkända.
    - **Inte konfigurerat** – Icke-företagswebbplatser kan öppnas på enheten

  - **Funktionssätt för Urklipp**  
    CSP: [Settings/ClipboardSettings](https://go.microsoft.com/fwlink/?linkid=872351)

    Välj vilka åtgärder för kopiera och klistra in som tillåts mellan den lokala datorn och den virtuella Application Guard-webbläsaren. Alternativen är:
    - **Inte konfigurerat**  
    - **Blockera kopiera och klistra in mellan dator och webbläsare** (*standard*) – Blockerar båda. Data kan inte överföras mellan datorn och den virtuella webbläsaren.
    - **Tillåt endast kopiera och klistra in från webbläsare till dator** – Data kan inte överföras från datorn till den virtuella webbläsaren.
    - **Tillåt endast kopiera och klistra in från dator till webbläsare** – Data kan inte överföras från den virtuella webbläsaren till värddatorn.
    - **Tillåt kopiera och klistra in mellan dator och webbläsare** – Ingen blockering för innehåll finns.

- **Princip för nätverksisolering i Windows**  
  CSP: [Policy CSP – NetworkIsolation](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-networkisolation)

  Ange en lista över *Nätverksdomäner*, som är Enterprise-resurser som finns i molnet och som Application Guard behandlar som företagswebbplatser
  - **Konfigurera** (*standard*)
  - **Inte konfigurerat**

  När du har angett *Konfigurera* kan du definiera *Nätverksdomäner*.

  - **Nätverksdomäner**  
    Välj **Lägg till** och ange domäner, IP-adressintervall och nätverksgränser. *securitycenter.windows.com* konfigureras som standard.

## <a name="bitlocker"></a>BitLocker

Mer information finns i [BitLocker-grupprincipinställningar](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-group-policy-settings) i Windows-dokumentationen.

- **Kräv att lagringskort ska krypteras (endast mobil)**  
  CSP: [RequireStorageCardEncryption](https://go.microsoft.com/fwlink/?linkid=872524)

  Den här inställningen gäller endast för Windows Mobile- och Mobile Enterprise SKU-enheter.
  - **Ja** (*standard*) – Kryptering på minneskort krävs för mobila enheter.
  - **Inte konfigurerat** – Inställningen återgår till operativsystemstandard, vilket är att inte kräva kryptering på lagringskort.

- **Aktivera fullständig diskkryptering för operativsystem och fasta dataenheter**  
  CSP: [RequireDeviceEncryption](https://go.microsoft.com/fwlink/?linkid=872523)

  Om enheten krypterades innan den här principen tillämpades vidtas ingen extra åtgärd. Om krypteringsmetoden och alternativen stämmer överens med den här principen ska konfigurationen returnera lyckat resultat. Om ett alternativ för BitLocker-konfiguration på plats inte matchar den här principen kommer konfigurationen troligen att returnera ett fel.
  
  Om du vill tillämpa den här principen på en disk som redan är krypterad dekrypterar du enheten och tillämpar MDM-principen igen. Windows standard är att inte kräva BitLocker-diskkryptering, men för Azure AD-anslutning och Microsoft Account (MSA)-registrering/-inloggning kan automatisk kryptering tillämpa aktivering av BitLocker på XTS-AES 128-bitars kryptering.

  - **Ja** (*standard*) – Framtvinga användning av BitLocker.
  - **Inte konfigurerat** – Ingen BitLocker-kryptering sker.

- **Princip för BitLocker på systemenheter**  
  [BitLocker-grupprincipinställningar](https://go.microsoft.com/fwlink/?linkid=2067025)

  - **Konfigurera** (*standard*)
  - **Inte konfigurerat**

  När du har angett *Konfigurera* kan du konfigurera *Konfigurera krypteringsmetod för operativsystemenheter*.

  - **Konfigurera krypteringsmetod för operativsystemenheter**  
    CSP: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  
    Den här inställningen är tillgänglig när *Princip för BitLocker på systemenheter* har angetts till *Konfigurera*.  

    Konfigurera krypteringsmetod och krypteringsgrad för systemenheter.  *XTS-AES 128-bitars* är Windows standardkrypteringsmetod och det rekommenderade värdet.

    - **Ej konfigurerat** (*standard*)
    - **AES 128-bitars CBC**
    - **AES 256-bitars CBC**
    - **AES 128-bitars XTS**
    - **AES 256-bitars XTS**

- **Princip för BitLocker på fasta enheter**  
  [BitLocker-grupprincipinställningar](https://go.microsoft.com/fwlink/?linkid=2067018)

  - **Konfigurera** (*standard*)
  - **Inte konfigurerat**

  När du har angett *Konfigurera* kan du konfigurera *Blockera skrivåtkomst till fasta dataenheter som inte skyddas av BitLocker* och *Konfigurera krypteringsmetod för fasta dataenheter*.

  - **Blockera skrivåtkomst till fasta dataenheter som inte skyddas av BitLocker**  
    CSP: [FixedDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872534)  
    Den här inställningen är tillgänglig när *Princip för BitLocker på fasta enheter* har angetts till *Konfigurera*.

    - **Inte konfigurerat** (*standard*) – Data kan skrivas till icke-krypterade fasta enheter.
    - **Ja** – Windows tillåter inte att data skrivs till fasta enheter som inte är BitLocker-skyddade. Om en fast enhet inte är krypterad måste användaren slutföra installationsguiden för BitLocker för enheten innan skrivåtkomst beviljas.

  - **Konfigurera krypteringsmetod för fasta dataenheter**  
    CSP: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  
    Den här inställningen är tillgänglig när *Princip för BitLocker på fasta enheter* har angetts till *Konfigurera*.

    Konfigurera krypteringsmetod och krypteringsgrad för fasta dataenhetsdiskar. *XTS-AES 128-bitars* är Windows standardkrypteringsmetod och det rekommenderade värdet.

    - **Ej konfigurerat** (*standard*)
    - **AES 128-bitars CBC**
    - **AES 256-bitars CBC**
    - **AES 128-bitars XTS**
    - **AES 256-bitars XTS**

- **Princip för BitLocker på flyttbara enheter**  
  [BitLocker-grupprincipinställningar](https://go.microsoft.com/fwlink/?linkid=2067140)

  - **Konfigurera** (*standard*)
  - **Inte konfigurerat**

  När du har angett *Konfigurera* kan du konfigurera *Konfigurera krypteringsmetod för flyttbara dataenheter* och *Blockera skrivåtkomst till flyttbara dataenheter som inte skyddas av BitLocker*.

  - **Konfigurera krypteringsmetod för flyttbara dataenheter**  
    CSP: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  
    Den här inställningen är tillgänglig när *Princip för BitLocker på flyttbara enheter* har angetts till *Konfigurera*.

    Konfigurera krypteringsmetod och krypteringsgrad för flyttbara dataenhetsdiskar. *XTS-AES 128-bitars* är Windows standardkrypteringsmetod och det rekommenderade värdet.

    - **Inte konfigurerat**
    - **AES 128-bitars CBC**
    - **AES 256-bitars CBC** (*standard*)
    - **AES 128-bitars XTS**
    - **AES 256-bitars XTS**

  - **Blockera skrivåtkomst till flyttbara dataenheter som inte skyddas av BitLocker**  
    CSP: [RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)  
    Den här inställningen är tillgänglig när *Princip för BitLocker på flyttbara enheter* har angetts till *Konfigurera*.

    - **Inte konfigurerat** (*standard*) – Data kan skrivas till icke-krypterade flyttbara enheter.  
    - **Ja** – Windows tillåter inte att data skrivs till flyttbara enheter som inte är BitLocker-skyddade. Om en flyttbar enhet inte är krypterad måste användaren slutföra installationsguiden för BitLocker för enheten innan skrivåtkomst beviljas.

## <a name="browser"></a>Webbläsare

- **Require SmartScreen for Microsoft Edge** (Kräv SmartScreen för Microsoft Edge)  
  CSP: [Browser/AllowSmartScreen](https://go.microsoft.com/fwlink/?linkid=2067029)

  - **Ja** (*standard*) – Använd SmartScreen för att skydda användarna mot potentiella nätfiskeförsök och skadlig programvara.
  - **Inte konfigurerat**

- **Block malicious site access** (Blockera åtkomst till skadliga webbplatser)  
  CSP: [Browser/PreventSmartScreenPromptOverride](https://go.microsoft.com/fwlink/?linkid=2067040)  

  - **Ja** (*standard*) – Blockera användare från att ignorera Microsoft Defender SmartScreen-filtervarningar och blockera dem från att gå till webbplatsen.
  - **Inte konfigurerat**

- **Block unverified file download** (Blockera nedladdning av overifierade filer)  
  CSP: [Browser/PreventSmartScreenPromptOverrideForFiles](https://go.microsoft.com/fwlink/?linkid=2067023)  

  - **Ja** (*standard*) – Blockera användare från att ignorera Microsoft Defender SmartScreen-filtervarningar och blockera dem från att ladda ned overifierade filer.
  - **Inte konfigurerat**

## <a name="data-protection"></a>Dataskydd

- **Block direct memory access** (Blockera direkt minnesåtkomst)  
  CSP: [DataProtection/AllowDirectMemoryAccess](https://go.microsoft.com/fwlink/?linkid=2067031)  

  Den här principinställningen tillämpas endast när BitLocker- eller enhetskryptering är aktiverat.

  - **Ja** (*standard*) – Blockera direkt minnesåtkomst (DMA) för alla underordnade PCI-portar med enhetsbyte vid drift tills en användare loggar in i Windows. När en användare har loggat in räknar Windows upp PCI-enheterna som är anslutna till PCI-portarna med hot plug-stöd. Varje gång användaren låser datorn blockeras DMA på PCI-portarna med hot plug-stöd utan underordnade enheter tills användaren loggar in igen. Enheter som räknades upp när datorn var upplåst fortsätter att fungera tills de kopplas från.
  - **Inte konfigurerat**

## <a name="device-guard"></a>Device Guard  

- **Aktivera Credential Guard**  
  CSP: [DeviceGuard/ConfigureSystemGuardLaunch](https://go.microsoft.com/fwlink/?linkid=872424)

  Credential Guard använder Windows Hypervisor för att tillhandahålla skydd, vilket kräver att funktionerna för säker start och DMA-skydd fungerar, vilket kräver att maskinvarukraven uppfylls.

  - **Inte konfigurerat** – Inaktivera användningen av Credential Guard, som är Windows-standard.
  - **Aktivera med UEFI-lås** (*standard*) – Aktivera Credential Guard och tillåt inte att det inaktiveras via fjärranslutning, eftersom den kvarstående konfigurationen i UEFI måste rensas manuellt.
  - **Aktivera utan UEFI-lås** – Aktivera Credential Guard och tillåt att det inaktiveras utan fysisk åtkomst till datorn.

## <a name="device-installation"></a>Enhetsinstallation

- **Hardware device installation by device identifiers** (Installation av maskinvaruenheter efter enhets-ID)  
  [DeviceInstallation/PreventInstallationOfMatchingDeviceIDs](https://go.microsoft.com/fwlink/?linkid=2066794)  
  
  Med den här principinställningen kan du ange en lista med ID:n för Plug and Play-maskinvara och kompatibla ID:n för enheter som Windows hindrar från att installeras. Den här inställningen har företräde framför alla andra principinställningar som tillåter att Windows installerar en enhet.  Om du aktiverar den här principinställningen på en fjärrskrivbordsserver påverkar principinställningen omdirigeringen av de angivna enheterna från en fjärrskrivbordsklient till fjärrskrivbordsservern.

  - **Inte konfigurerat**
  - **Tillåt installation av maskinvaruenheter** – Enheter kan installeras och uppdateras beroende på vad som tillåts eller förhindras av andra principinställningar.
  - **Blockera installation av maskinvaruenheter** (*standard*) – Windows hindras från att installera en enhet vars maskinvaru-ID eller kompatibelt ID visas i listan som du definierar.

  När du har angett *Blockera installation av maskinvaruenheter* kan du konfigurera *Ta bort matchande maskinvaruenheter* och *Maskinvaruenheters identifierare som har blockerats*.

  - **Remove matching hardware devices** (Ta bort matchande maskinvaruenheter)

    Den här inställningen är endast tillgänglig när *Hardware device installation by device identifiers* (Installation av maskinvaruenheter efter enhets-ID) har inställningen *Block hardware device installation* (Blockera installation av maskinvaruenheter).
    - **Ja**
    - **Inte konfigurerat**

  - **Hardware device identifiers that are blocked** (ID:n för blockerade maskinvaruenheter)  
    
    Den här inställningen är endast tillgänglig när *Hardware device installation by device identifiers* (Installation av maskinvaruenheter efter enhets-ID) har inställningen *Block hardware device installation* (Blockera installation av maskinvaruenheter).

    Välj **Lägg till** och ange sedan maskinvarans enhets-ID som du vill blockera.

- **Hardware device installation by setup classes** (Installation av maskinvaruenheter efter installationsklass)  
  CSP: [DeviceInstallation/AllowInstallationOfMatchingDeviceSetupClasses](https://go.microsoft.com/fwlink/?linkid=2067048)  
  
  Med den här principinställningen kan du ange en lista med klass-GUID för enhetsinstallation för enhetsdrivrutiner som Windows hindrar från att installeras. Den här inställningen har företräde framför alla andra principinställningar som tillåter att Windows installerar en enhet. Om du aktiverar den här principinställningen på en fjärrskrivbordsserver påverkar principinställningen omdirigeringen av de angivna enheterna från en fjärrskrivbordsklient till fjärrskrivbordsservern.

  - **Inte konfigurerat**
  - **Tillåt installation av maskinvaruenheter** – Windows kan installera och uppdatera enheter beroende på vad som tillåts eller förhindras av andra principinställningar.
  - **Blockera installation av maskinvaruenheter** (*standard*) – Windows hindras från att installera en enhet vars klass-GUID för installation visas i en lista som du definierar.

  När du har angett *Blockera installation av maskinvaruenheter* kan du konfigurera *Ta bort matchande maskinvaruenheter* och *ID:n för blockerade maskinvaruenheter*.

  - **Remove matching hardware devices** (Ta bort matchande maskinvaruenheter)

    Den här inställningen är endast tillgänglig när *Hardware device installation by device identifiers* (Installation av maskinvaruenheter efter enhets-ID) har inställningen *Block hardware device installation* (Blockera installation av maskinvaruenheter).
    - **Ja**
    - **Inte konfigurerat**

  - **Hardware device identifiers that are blocked** (ID:n för blockerade maskinvaruenheter)

    Den här inställningen är endast tillgänglig när *Hardware device installation by device identifiers* (Installation av maskinvaruenheter efter enhets-ID) har inställningen *Block hardware device installation* (Blockera installation av maskinvaruenheter).

    Välj **Lägg till** och ange sedan maskinvarans enhets-ID som du vill blockera.

## <a name="dma-guard"></a>DMA Guard

- **Uppräkning av externa enheter som är inkompatibla med Kernel DMA-skydd**  
  CSP: [DmaGuard/DeviceEnumerationPolicy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-dmaguard#dmaguard-deviceenumerationpolicy)

  Den här principen kan ge ökad säkerhet mot externa DMA-kompatibla enheter. Det möjliggör större kontroll över uppräkning av externa DMA-kompatibla enheter som inte är kompatibla med minnesisolering och sandbox-miljö för DMA-mappning/-enhet.
  
  Den här principen börjar bara gälla när Kernel DMA-skydd stöds och aktiveras av datorns inbyggda programvara. Kernel DMA-skydd är en plattformsfunktion som måste kunna hanteras av systemet vid tidpunkten för tillverkningen. Om du vill kontrollera om systemet har stöd för kernel DMA-skydd kontrollerar du fältet Kernel DMA-skydd på sammanfattningssidan i MSINFO32.exe.

  - **Inte konfigurerat** – (*standard*)
  - **Blockera alla**
  - **Tillåt alla**

## <a name="endpoint-detection-and-response"></a>Slutpunktsidentifiering och svar

Mer information om följande inställningar finns i [WindowsAdvancedThreatProtection](https://docs.microsoft.com/windows/client-management/mdm/windowsadvancedthreatprotection-csp) CSP i Windows-dokumentationen.

- **Exempeldelning för alla filer**  
  CSP: [Configuration/SampleSharing](https://docs.microsoft.com/windows/client-management/mdm/windowsadvancedthreatprotection-csp)

  Returnerar eller anger konfigurationsparametern för exempeldelning i Microsoft Defender Avancerat skydd.  
  
  - **Ja** (*standard*)
  - **Inte konfigurerat**

- **Skicka frekvensvärde för telemetrirapportering**  
  CSP: [Configuration/TelemetryReportingFrequency](https://docs.microsoft.com/windows/client-management/mdm/windowsadvancedthreatprotection-csp)

  Skicka frekvensvärde för telemetrirapportering för Microsoft Defender Avancerat skydd.  

  - **Ja** (*standard*)
  - **Inte konfigurerat**

## <a name="firewall"></a>Brandvägg

Mer information finns i [CSP-brandvägg](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp) i Windows-dokumentationen.

- **Inaktivera tillståndskänsligt filöverföringsprotokoll (FTP)**  
  CSP: [MdmStore/Global/DisableStatefulFtp](https://go.microsoft.com/fwlink/?linkid=872536)  

  - **Ja** (*standard*)
  - **Inte konfigurerat** – Brandväggen använder FTP för att kontrollera och filtrera sekundära nätverksanslutningar, vilket kan göra att brandväggsreglerna ignoreras.

- **Antal sekunder som en säkerhetsassociation kan vara inaktiv innan den tas bort**  
CSP: [MdmStore/Global/SaIdleTime](https://go.microsoft.com/fwlink/?linkid=872539)

  Ange hur länge säkerhetsassociationerna ska sparas efter det att nätverkstrafiken inte längre visas. När det inte har konfigurerats tar systemet bort en säkerhetsassociation när den har varit inaktiv i *300* sekunder (standard).
  
  Antalet måste vara från **300** till **3 600** sekunder.

- **Kodning för i förväg delad nyckel**  
  CSP: [MdmStore/Global/PresharedKeyEncoding](https://go.microsoft.com/fwlink/?linkid=872541)

   Om du inte kräver UTF-8 kommer i förväg delade nycklar initialt att kodas med UTF-8. Efter det kan enhetsanvändare välja en annan kodningsmetod.

  - **Inte konfigurerat**
  - **Inga**
  - **UTF8-** (*standard*)

- **Kontroll av lista över återkallade certifikat**  
  CSP: [MdmStore/Global/CRLcheck](https://go.microsoft.com/fwlink/?linkid=872548)

  Ange hur kontroll av listan över återkallade certifikat ska aktiveras.  

  - **Inte konfigurerat** (*standard*) – kontroll av listan över återkallade certifikat är inaktiverad.
  - **Inga**
  - **Försök**
  - **Kräv**

- **Paketkö**  
  CSP: [MdmStore/Global/EnablePacketQueue](https://go.microsoft.com/fwlink/?linkid=872551)

  Ange hur skalning för programvara på mottagarsidan aktiveras för den krypterade mottagningen och rensa flyttning av text framåt för scenariot med IPsec-tunnelgatewayen. Denna inställning säkerställer att paketordningen bevaras.

  - **Inte konfigurerat** (*standard*) – Paketköer återgår till klientens standardvärde, vilket är inaktiverad.
  - **Inaktiverad**
  - **Kö inkommande**
  - **Kö utgående**
  - **Kö båda**

- **Privat brandväggsprofil**  
  [2.2.2 FW_PROFILE_TYPE](https://go.microsoft.com/fwlink/?linkid=2067041)

  - **Konfigurera** (*standard*)
  - **Inte konfigurerat**

  När *Konfigurera* har angetts kan du konfigurera följande ytterligare inställningar.

  - **Inkommande anslutningar blockerade**  
    CSP: [/DefaultInboundAction](https://go.microsoft.com/fwlink/?linkid=872564)

    - **Ja** (*standard*)
    - **Inte konfigurerat**

  - **Unicast-svar på multicast-sändningar krävs**  
    CSP: [/DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

    - **Ja** (*standard*)
    - **Inte konfigurerat**

  - **Dolt läge krävs**  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Ja** (*standard*)
    - **Inte konfigurerat**

  - **Utgående anslutningar krävs**  
    CSP: [/DefaultOutboundAction](https://aka.ms/intune-firewall-outboundaction)

    - **Ja** (*standard*)
    - **Inte konfigurerat**

  - **Inkommande meddelanden blockerade**  
    CSP: [/DisableInboundNotifications](https://go.microsoft.com/fwlink/?linkid=872563)

    - **Ja** (*standard*)
    - **Inte konfigurerat**

  - **Globala portregler från sammanfogad grupprincip**  
    CSP: [/GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **Ja** (*standard*)
    - **Inte konfigurerat**

  - **Dolt läge blockerat**  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Ja** (*standard*)
    - **Inte konfigurerat**

  - **Brandväggen är aktiverad**  
    CSP: [/EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

    - **Inte konfigurerat**
    - **Blockerad**
    - **Tillåtet** (*standard*)

  - **Auktoriserade programregler från inte sammanfogad grupprincip**  
    CSP: [/AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **Ja** (*standard*)
    - **Inte konfigurerat**

  - **Regler för anslutningssäkerhet från inte sammanfogad grupprincip**  
    CSP: [/AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **Ja** (*standard*)
    - **Inte konfigurerat**

  - **Inkommande trafik krävs**  
    CSP: [/Shielded](https://go.microsoft.com/fwlink/?linkid=872561)

    - **Ja** (*standard*)
    - **Inte konfigurerat**

  - **Principregler från inte sammanfogad grupprincip**  
    CSP: [/AllowLocalPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872567)

    - **Ja** (*standard*)
    - **Inte konfigurerat**

- **Offentlig brandväggsprofil**  
  [2.2.2 FW_PROFILE_TYPE](https://go.microsoft.com/fwlink/?linkid=2067143)

  - **Konfigurera** (*standard*)
  - **Inte konfigurerat**

  När *Konfigurera* har angetts kan du konfigurera följande ytterligare inställningar.

  - **Inkommande anslutningar blockerade**  
    CSP: [/DefaultInboundAction](https://go.microsoft.com/fwlink/?linkid=872564)

    - **Ja** (*standard*)
    - **Inte konfigurerat**

  - **Unicast-svar på multicast-sändningar krävs**  
    CSP: [/DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

    - **Ja** (*standard*)
    - **Inte konfigurerat**

  - **Dolt läge krävs**  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Ja** (*standard*)
    - **Inte konfigurerat**

  - **Utgående anslutningar krävs**  
    CSP: [/DefaultOutboundAction](https://aka.ms/intune-firewall-outboundaction)

    - **Ja** (*standard*)
    - **Inte konfigurerat**

  - **Auktoriserade programregler från inte sammanfogad grupprincip**  
    CSP: [/AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **Ja** (*standard*)
    - **Inte konfigurerat**

  - **Inkommande meddelanden blockerade**  
    CSP: [/DisableInboundNotifications](https://go.microsoft.com/fwlink/?linkid=872563)

    - **Ja** (*standard*)
    - **Inte konfigurerat**

  - **Globala portregler från sammanfogad grupprincip**  
    CSP: [/GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **Ja** (*standard*)
    - **Inte konfigurerat**

  - **Dolt läge blockerat**  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Ja** (*standard*)
    - **Inte konfigurerat**

  - **Brandväggen är aktiverad**  
    CSP: [/EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

    - **Inte konfigurerat**
    - **Blockerad**
    - **Tillåtet** (*standard*)

  - **Regler för anslutningssäkerhet från inte sammanfogad grupprincip**  
    CSP: [/AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **Ja** (*standard*)
    - **Inte konfigurerat**

  - **Inkommande trafik krävs**  
    CSP: [/Shielded](https://go.microsoft.com/fwlink/?linkid=872561)

    - **Ja** (*standard*)
    - **Inte konfigurerat**

  - **Principregler från inte sammanfogad grupprincip**  
    CSP: [/AllowLocalPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872567)

    - **Ja** (*standard*)
    - **Inte konfigurerat**

- **Domän för brandväggsprofil**  
  CSP: [2.2.2 FW_PROFILE_TYPE](https://go.microsoft.com/fwlink/?linkid=2066796)

  - **Unicast-svar på multicast-sändningar krävs**  
    CSP: [/DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

  - **Auktoriserade programregler från inte sammanfogad grupprincip**  
    CSP: [/AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **Ja** (*standard*)
    - **Inte konfigurerat**  

  - **Inkommande meddelanden blockerade**  
    CSP: [/DisableInboundNotifications](https://go.microsoft.com/fwlink/?linkid=872563)

    - **Ja** (*standard*)
    - **Inte konfigurerat**

  - **Globala portregler från sammanfogad grupprincip**  
    CSP: [/GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **Ja** (*standard*)
    - **Inte konfigurerat**

  - **Dolt läge blockerat**  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Ja** (*standard*)
    - **Inte konfigurerat**

  - **Brandväggen är aktiverad**  
    CSP: [/EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

    - **Inte konfigurerat**
    - **Blockerad**
    - **Tillåtet** (*standard*)

  - **Regler för anslutningssäkerhet från inte sammanfogad grupprincip**  
    CSP: [/AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **Ja** (*standard*)
    - **Inte konfigurerat**

  - **Principregler från inte sammanfogad grupprincip**  
    CSP: [/AllowLocalPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872567)

    - **Ja** (*standard*)
    - **Inte konfigurerat**

## <a name="microsoft-defender"></a>Microsoft Defender

- **Kör daglig snabbsökning**  
  CSP: [Defender/ScheduleQuickScanTime](https://go.microsoft.com/fwlink/?linkid=2114053&clcid=0x409)
  
   Konfigurera när den dagliga snabbsökningen ska köras. Som standard är genomsökningen inställd på att köras **02:00**.

- **Schemalagd starttid för genomsökning**  
  
  Som standard är det här värdet inställt på **02:00**.

- **Konfigurera låg CPU-prioritet för schemalagda genomsökningar**  
  CSP: [Defender/EnableLowCPUPriority](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-enablelowcpupriority)  

  -**Ja** (*standard*)
  - **Inte konfigurerat**

- **Blockera Office-kommunikationsprogram från att skapa underordnade processer**  
  [Skydda enheter från angrepp](https://go.microsoft.com/fwlink/?linkid=874499)  

  Den här ASR-regeln styrs via följande GUID: 26190899-1602-49e8-8b27-eb1d0a1ce869.
  - **Inte konfigurerat** – Windows standardvärde är återställt, för att inte blockera skapandet av underordnade processer.
  - **Användardefinierad**
  - **Aktivera** (*standard*) – Office-kommunikationsprogram blockeras från att skapa underordnade processer.
  - **Granskningsläge** – Windows-händelser höjs i stället för att blockera underordnade processer.

- **Blockera Adobe Reader från att skapa underordnade processer**  
  [Minska attackytan med regler för minskning av attackytan](https://go.microsoft.com/fwlink/?linkid=853979)  

  - **Inte konfigurerat** – Windows standardvärde är återställt, att inte blockera skapandet av underordnade processer.
  - **Användardefinierad**
  - **Aktivera** (*standard*) – Adobe Reader är blockerat från att skapa underordnade processer.
  - **Granskningsläge** – Windows-händelser höjs i stället för att blockera underordnade processer.

- **Sök igenom inkommande e-postmeddelanden**  
  CSP: [Defender/AllowEmailScanning](https://go.microsoft.com/fwlink/?linkid=2114052&clcid=0x409)

  - **Ja** (*standard*) – E-postlåda och e-postfiler som PST, DBX, MNX, MIME och BINHEX genomsöks.
  - **Inte konfigurerat** – Inställningen återgår till klientens standard att e-postfiler inte genomsöks.

- **Starta realtidsskydd**  
  CSP: [Defender/AllowRealtimeMonitoring](https://go.microsoft.com/fwlink/?linkid=2114050&clcid=0x409)

  - **Ja** (*standard*) – Övervakning i realtid upprätthålls och användaren kan inte inaktivera den.
  - **Inte konfigurerat** – Inställningen återgår till klientens standard, vilken är aktiverad, men användaren kan ändra den. Använd en anpassad URI för att inaktivera realtidsövervakning.

- **Antal dagar (0–90) som skadlig kod ska bevaras i karantän**  
  CSP: [Defender/DaysToRetainCleanedMalware](https://go.microsoft.com/fwlink/?linkid=2114055&clcid=0x409)

  Konfigurera antalet dagar som objekt ska behållas i mappen karantän innan de tas bort. Standardvärdet är noll (**0**), vilket resulterar i att filer i karantän aldrig tas bort.

- **Genomsökningsschema för Defender-system**  
  CSP: [Defender/ScheduleScanDay](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulescanday)

  Schemalägg vilken dag Defender ska söka igenom enheter. Som standard är genomsökningen **användardefinierad**, men kan ställas in på *Varje dag*, valfri veckodag eller *Ingen schemalagd genomsökning*.

- **Ytterligare utökad tid (0–50 sekunder) för tidsgränsen för molnskydd**  
  CSP: [Defender/CloudExtendedTimeout](https://go.microsoft.com/fwlink/?linkid=2113940&clcid=0x409)

  Defender Antivirus blockerar automatiskt misstänkta filer i 10 sekunder så att det kan genomsöka filerna i molnet för att kontrollera att de är säkra. Med den här inställningen kan du lägga till upp till 50 ytterligare sekunder till tidsgränsen.  Som standard anges tidsgränsen till noll (**0**).

- **Sök igenom mappade nätverksdrivrutiner vid fullständig genomsökning**  
  CSP: [Defender/AllowFullScanOnMappedNetworkDrives](https://go.microsoft.com/fwlink/?linkid=2113945&clcid=0x409)

  - **Ja** (*standard*) – Under en fullständig genomsökning inkluderas mappade nätverksenheter.
  - **Inte konfigurerat** – Klienten återgår till standardvärdet, vilket inaktiverar genomsökning på mappade nätverksenheter.

- **Aktivera nätverksskydd**  
  CSP: [Defender/EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=2113939&clcid=0x409)
  
  - **Ja** (*standard*) – Blockera skadlig trafik som identifierats av signaturer i NIS (Network Inspection System).
  - **Inte konfigurerat**

- **Genomsök alla nedladdade filer och bifogade filer**  
  CSP: [Defender/AllowIOAVProtection](https://go.microsoft.com/fwlink/?linkid=2113934&clcid=0x409)

  - **Ja** (*standard*) – Alla nedladdade filer och bifogade filer söks igenom. Inställningen återgår till klientens standard, vilken är aktiverad, men användaren kan ändra den. Om du vill inaktivera den här inställningen använder du en anpassad URI.
  - **Inte konfigurerat** – Inställningen återgår till klientens standard, vilken är aktiverad, men användaren kan ändra den. Om du vill inaktivera den här inställningen använder du en anpassad URI.

::: zone-end
::: zone pivot="atp-april-2020"

- **Blockera åtkomstskydd**  
  CSP: [Defender/AllowOnAccessProtection](https://go.microsoft.com/fwlink/?linkid=2113935&clcid=0x409)

  - **Ja**
  - **Ej konfigurerat** (*standard*)

::: zone-end
::: zone pivot="atp-march-2020"

- **Blockera åtkomstskydd**  
  CSP: [Defender/AllowOnAccessProtection](https://go.microsoft.com/fwlink/?linkid=2113935&clcid=0x409)

  - **Ja** (*standard*)
  - **Inte konfigurerat**

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"

- **Genomsök webbläsarskript**  
  CSP: [Defender/AllowScriptScanning](https://go.microsoft.com/fwlink/?linkid=2114054&clcid=0x409)

  - **Ja** (*standard*) – Skriptgenomsökningsfunktionen i Microsoft Defender tillämpas och användaren kan inte inaktivera den.
  - **Inte konfigurerat** – Inställningen återgår till klientens standardvärde, vilket är att aktivera skriptgenomsökning, men användaren kan inaktivera den.

- **Blockera användaråtkomst till Microsoft Defender-app**  
  CSP: [Defender/AllowUserUIAccess](https://go.microsoft.com/fwlink/?linkid=2114043&clcid=0x409)

  - **Ja** (*standard*) – Användargränssnittet för Microsoft Defender är inte tillgängligt och aviseringar visas inte
  - **Inte konfigurerat** – När det är inställt på Ja, är användargränssnittet för Windows Defender inte tillgängligt och aviseringar visas inte. När inställningen är Inte konfigurerat återgår inställningen till klientens standardvärde där gränssnitt och aviseringar tillåts

- **Högsta tillåtna processoranvändning (0–100 procent) per genomsökning**  
  CSP: [Defender/AvgCPULoadFactor](https://go.microsoft.com/fwlink/?linkid=2114046&clcid=0x409)

  Ange i procent den maximala CPU-mängd som ska användas för en genomsökning. Standard är **50**.

- **Skanningstyp**  
  CSP: [Defender/ScanParameter](https://go.microsoft.com/fwlink/?linkid=2114045&clcid=0x409)

  - **Användardefinierad**
  - **Inaktiverad**
  - **Snabbsökning** (*standard*)
  - **Fullständig genomsökning**

- **Ange hur ofta (0–24 timmar) sökning ska ske efter säkerhetsinsiktsuppdateringar**  
  CSP: [Defender/SignatureUpdateInterval](https://go.microsoft.com/fwlink/?linkid=2113936&clcid=0x409)

  Ange hur ofta du vill söka efter uppdaterade signaturer, i timmar. Med värdet 1 sker till exempel kontroll varje timme. Värdet 2 kommer att kontrollera varannan timme och så vidare.

  Om inget värde har definierats använder enheterna klientstandarden på **8** timmar.

- **Medgivande i Defender för överföring av dataprover**  
  CSP: [Defender/SubmitSamplesConsent](https://go.microsoft.com/fwlink/?linkid=2067131)

  Kontrollerar nivån för användarmedgivande i Microsoft Defender för överföring av data. Om nödvändigt godkännande redan har beviljats, skickar Microsoft Defender dem. Annars (och om användaren har valt att aldrig bli tillfrågad) startas användargränssnittet för att be om användarens medgivande (när *Molnlevererat skydd* är inställt på *Ja*) innan data skickas.

  - **Skicka säkra exempel automatiskt** (*standard*)
  - **Fråga alltid**
  - **Skicka aldrig**
  - **Skicka alla exempel automatiskt**

- **Nivå för molnlevererat skydd**  
  CSP: [CloudBlockLevel](https://go.microsoft.com/fwlink/?linkid=2113942)

  Konfigurera hur aggressivt Defender Antivirus ska blockera och genomsöka misstänkta filer.
  - **Inte konfigurerad** (*standard*) – Standardnivå för blockering i Defender.
  - **Hög** – Aggressiv blockering av okända filer och optimering av klientprestanda, med större risk för falskt positiva resultat.
  - **Hög plus** – Aggressiv blockering av okända filer och tillämpning av ytterligare skyddsåtgärder som kan påverka klientprestandan.
  - **Nolltolerans** – Blockerar alla okända körbara filer.

- **Sök igenom arkivfiler**  
  CSP: [Defender/AllowArchiveScanning](https://go.microsoft.com/fwlink/?linkid=2114047&clcid=0x409)

  - **Ja** (*standard*) – Genomsökning av arkivfiler som ZIP-eller CAB-filer tillämpas.
  - **Inte konfigurerat** – Inställningen återgår till klientens standardvärde, som är att söka igenom arkiverade filer, men användaren kan inaktivera genomsökning.

- **Aktivera beteendeövervakning**  
  CSP: [Defender/AllowBehaviorMonitoring](https://go.microsoft.com/fwlink/?linkid=2114048&clcid=0x409)

  - **Ja** (*standard*) – Övervakning av beteende upprätthålls och användaren kan inte inaktivera den.
  - **Inte konfigurerat** – Inställningen återgår till klientens standard, vilken är aktiverad, men användaren kan ändra den. Använd en anpassad URI för att inaktivera realtidsövervakning.
  
- **Genomsök flyttbara enheter vid fullständig genomsökning**  
  CSP: [Defender/AllowFullScanRemovableDriveScanning](https://go.microsoft.com/fwlink/?linkid=2113946&clcid=0x409)

  - **Ja** (*standard*) – Under en fullständig genomsökning genomsöks flyttbara enheter (t.ex. USB-minnen).
  - **Inte konfigurerat** – Inställningen återgår till klientens standardvärde, vilket är genomsökning av flyttbara enheter, men användaren kan inaktivera den här genomsökningen.
  
- **Genomsök nätverksfiler**  
  CSP: [Defender/AllowScanningNetworkFiles](https://go.microsoft.com/fwlink/?linkid=2114049&clcid=0x409)

  - **Ja** (*standard*) – Microsoft Defender genomsöker nätverksfiler.
  - **Inte konfigurerat** – Klienten återgår till standardvärdet, vilket inaktiverar genomsökning av nätverksfiler.
  
- **Defender potentially unwanted app action** (Potentiellt oönskad appåtgärd i Defender)  
  CSP: [Defender/PUAProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-puaprotection)

  Ange identifieringsnivå för potentiellt oönskade appar (PUA). Defender varnar användare när potentiellt oönskad programvara laddas ned eller försöker installeras på en enhet.
  - **Standard för enheten**
  - **Blockera** (*standard*) – Identifierade objekt blockeras och visas i historiken tillsammans med andra hot.
  - **Granska** – Defender identifierar potentiellt oönskade program men vidtar inga åtgärder. Du kan läsa information om vilka program som Windows Defender skulle ha vidtagit åtgärder mot genom att söka efter händelser som har skapats av Defender i Loggboken.

- **Aktivera molnlevererat skydd**  
  CSP: [AllowCloudProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  Som standard skickar Defender på Windows 10 Desktop-enheter information till Microsoft om eventuella problem som identifieras. Microsoft analyserar informationen för att lära sig mer om problem som påverkar dig och andra kunder och erbjuda bättre lösningar.

  - **Ja** (*standard*) – Molnlevererat skydd är aktiverat.  Enhetsanvändare kan inte ändra den här inställningen.
  - **Inte konfigurerat** – Inställningen återställs till systemets standard.

- **Blockera Office-program från att infoga kod i andra processer**  
  [Skydda enheter från angrepp](https://go.microsoft.com/fwlink/?linkid=872974)

  Den här ASR-regeln styrs via följande GUID: 75668C1F-73B5-4CF0-BB93-3ECF5CB7CC84
  - **Inte konfigurerat** – Inställningen återgår till Windows standardvärde, som är inaktiverad.
  - **Blockera** (*standard*) – Office-program blockeras från att infoga kod i andra processer.
  - **Granskningsläge** – Windows-händelser höjs i stället för att blockera.

- **Blockera Office-program från att skapa körbart innehåll**  
  [Skydda enheter från angrepp](https://go.microsoft.com/fwlink/?linkid=872975)

  Den här ASR-regeln styrs via följande GUID: 3B576869-A4EC-4529-8536-B80A7769E899
  - **Inte konfigurerat** – Inställningen återgår till Windows standardvärde, som är inaktiverad.
  - **Blockera** (*standard*) – Office-program blockeras från att skapa körbart innehåll.
  - **Granskningsläge** – Windows-händelser höjs i stället för att blockera.
  
- **Blockera JavaScript eller VBScript från att starta nedladdat körbart innehåll**  
  [Skydda enheter från angrepp](https://go.microsoft.com/fwlink/?linkid=872979)

   Den här ASR-regeln styrs via följande GUID: D3E037E1-3EB8-44C8-A917-57927947596D
  - **Inte konfigurerat** – Inställningen återgår till Windows standardvärde, som är inaktiverad.
  - **Blockera** (*standard*) – Defender blockerar JavaScript- eller VBScript-filer som har laddats ned från Internet från att köras.
  - **Granskningsläge** – Windows-händelser höjs i stället för att blockera.
  
- **Aktivera nätverksskydd**  
  CSP: [Defender/EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=872618)

  - **Inte konfigurerat** – Inställningen återgår till Windows standardvärde, som är inaktiverad.
  - **Användardefinierad**
  - **Aktivera** – Nätverksskydd är aktiverat för alla användare i systemet.
  - **Gransknings läge** (*standard*) – Användare blockeras inte från farliga domäner och Windows-händelser höjs i stället.

- **Blockera obetrodda och osignerade processer som körs via USB**  
  [Skydda enheter från angrepp](https://go.microsoft.com/fwlink/?linkid=874502)

  Den här ASR-regeln styrs via följande GUID: b2b3f03d-6a65-4f7b-a9c7-1c7ef74a9ba4
  - **Inte konfigurerat** – Inställningen återgår till Windows standardvärde, som är inaktiverad.
  - **Blockera** (*standard*) – Obetrodda och osignerade processer som körs från en USB-enhet blockeras.
  - **Granskningsläge** – Windows-händelser höjs i stället för att blockera.

- **Blockera stöld av autentiseringsuppgifter från det lokala säkerhetsundersystemet i Windows (lsass.exe)**  
  [Skydda enheter från angrepp](https://go.microsoft.com/fwlink/?linkid=874499)

  Den här ASR-regeln styrs via följande GUID: 9e6c4e1f-7d60-472f-ba1a-a39ef669e4b2
  - **Inte konfigurerat** – Inställningen återgår till Windows standardvärde, som är inaktiverad.
  - **Användardefinierad**
  - **Aktivera** (*standard*) – Försök att stjäla autentiseringsuppgifter via lsass.exe blockeras.
  - **Gransknings läge** – Användare blockeras inte från farliga domäner och Windows-händelser höjs i stället.

- **Blockera körbart innehåll från e-postklient och webbaserad e-post**  
  [Skydda enheter från angrepp](https://go.microsoft.com/fwlink/?linkid=872980)

  - **Inte konfigurerat** – Inställningen återgår till Windows standardvärde, som är inaktiverad.
  - **Blockera** (*standard*) – Körbart innehåll från e-postklient och webbaserad e-post blockeras.
  - **Granskningsläge** – Windows-händelser höjs i stället för att blockera.

- **Blockera Office-program från att skapa underordnade processer**  
  [Skydda enheter från angrepp](https://go.microsoft.com/fwlink/?linkid=872976)

  Den här ASR-regeln styrs via följande GUID: D4F940AB-401B-4EFC-AADC-AD5F3C50688A
  - **Inte konfigurerat** – Inställningen återgår till Windows standardvärde, som är inaktiverad.
  - **Blockera** (*standard*)
  - **Granskningsläge** – Windows-händelser höjs i stället för att blockera.

- **Blockera körning av potentiellt dolda skript (js/vbs/ps)**  
  [Skydda enheter från angrepp](https://go.microsoft.com/fwlink/?linkid=872978)

  Den här ASR-regeln styrs via följande GUID: 5BEB7EFE-FD9A-4556-801D-275E5FFC04CC
  - **Inte konfigurerat** – Inställningen återgår till Windows standardvärde, som är inaktiverad.
  - **Blockera** (*standard*) – Defender blockerar körning av dolda skript.
  - **Granskningsläge** – Windows-händelser höjs i stället för att blockera.

- **Blockera Win32-API-anrop från Office-makron**  
  [Skydda enheter från angrepp](https://go.microsoft.com/fwlink/?linkid=872977)

  Den här ASR-regeln styrs via följande GUID: 92E97FA1-2EDF-4476-BDD6-9DD0B4DDDC7B
  - **Inte konfigurerat** – Inställningen återgår till Windows standardvärde, som är inaktiverad.
  - **Blockera** (*standard*) – Office-makron blockeras från att använda Win32 API-anrop.
  - **Granskningsläge** – Windows-händelser höjs i stället för att blockera.

## <a name="microsoft-defender-security-center"></a>Microsoft Defender Security Center

- **Blockera användare från att redigera gränssnittet för Exploit Guard Protection**  
  CSP: [WindowsDefenderSecurityCenter/DisallowExploitProtectionOverride](https://go.microsoft.com/fwlink/?linkid=2067239)

  - **Ja** (*standard*) – Förhindra användare från att göra ändringar i inställningsområdet för sårbarhetsskydd i Microsoft Defender Security Center.
  - **Inte konfigurerat** – Lokala användare göra ändringar i inställningsområdet för sårbarhetsskydd.

## <a name="smart-screen"></a>Smart skärm

- **Blockera användare från att ignorera SmartScreen-varningar**  
  CSP: [SmartScreen/PreventOverrideForFilesInShell](https://go.microsoft.com/fwlink/?linkid=872783)

   Den här inställningen kräver att inställningen Aktivera Windows SmartScreen är inställd på Ja.
  - **Ja** (*standard*) – SmartScreen är aktiverat och användare kan inte kringgå varningar för filer eller skadliga appar.
  - **Inte konfigurerat** – Användare kan ignorera SmartScreen-varningar för filer och skadliga appar.

- **Kräv appar endast från Store**  

  - **Ja** (*standard*)
  - **Inte konfigurerat**

- **Aktivera Windows SmartScreen**  
  CSP: [SmartScreen/EnableSmartScreenInShell](https://go.microsoft.com/fwlink/?linkid=872784)

  - **Ja** (*standard*) – Framtvinga användning av SmartScreen för alla användare.
  - **Inte konfigurerat** – Inställningen återgår till Windows standardvärde, vilket är att aktivera SmartScreen, men användare kan ändra inställningen. Om du vill inaktivera SmartScreen använder du en anpassad URI.

## <a name="windows-hello-for-business"></a>Windows Hello för företag

Mer information finns i [PassportForWork CSP](https://docs.microsoft.com/windows/client-management/mdm/passportforwork-csp) i Windows-dokumentationen.

- **Blockera Windows Hello för företag**  

   Windows Hello för företag är en alternativ metod för att logga in till Windows genom att ersätta lösenord, smartkort och virtuella smartkort.

  - **Inte konfigurerat** – Enheter etablerar Windows Hello för företag, som är Windows standardvärde.
  - **Inaktiverad** (*standard*) – Enheter etablerar Windows Hello för företag.
  - **Aktiverad** – Enheter etablerar inte Windows Hello för företag för någon användare.

  När värdet är *Inaktiverad* kan du konfigurera följande inställningar:

  - **Gemener i PIN-kod**  
    - **Inte tillåtet**
    - **Obligatoriskt**
    - **Tillåtet** (*standard*)

  - **Specialtecken i PIN-kod**
    - **Inte tillåtet**
    - **Obligatoriskt**
    - **Tillåtet** (*standard*)

  - **Versaler i PIN-kod**
    - **Inte tillåtet**
    - **Obligatoriskt**
    - **Tillåtet** (*standard*)

::: zone-end

## <a name="next-steps"></a>Nästa steg

- [Läs mer om säkerhetsbaslinjer](security-baselines.md)
- [Undvika konflikter](security-baselines.md#avoid-conflicts)
- [Felsöka principer och profiler i Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)