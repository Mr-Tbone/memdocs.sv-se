---
title: Policyinställningar för diskkryptering i Intunes slutpunktssäkerhet | Microsoft Docs
description: Policyinställningar för diskkryptering i för BitLocker och FileVault i slutpunktssäkerheten i Microsoft Intune
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
ms.openlocfilehash: 3760aa9820495db6c2460bf2e6d2e9a08d705a10
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/18/2020
ms.locfileid: "86462039"
---
# <a name="disk-encryption-policy-settings-for-endpoint-security-in-intune"></a>Policyinställningar för diskkryptering i Intunes slutpunktssäkerhet

Visa de inställningar du kan konfigurera i profiler för policyn *Diskkryptering* i noden Endpoint Security i Intune inom ramen för [Endpoint Security-policyn](../protect/endpoint-security-policy.md).

Plattformar och profiler som stöds:

- **macOS**:
  - Profil: **FileVault**
- **Windows 10 och senare**:
  - Profil: **BitLocker**

## <a name="filevault"></a>FileVault

### <a name="encryption"></a>Kryptering

**Aktivera FileVault**  
- **Ej konfigurerat** (*standard*)
- **Ja** – aktivera fullständig diskkryptering med hjälp av XTS-AES 128 och FileVault på enheter som kör macOS 10.13 eller senare. FileVault aktiveras när användaren loggar ut från enheten.

  När du anger *Ja* kan du konfigurera ytterligare inställningar för FileVault.

  - Återställningsnycklar av **typen**
    *Privat nyckel* skapas för enheter. Konfigurera följande inställningar för den personliga nyckeln:

    - **Rotering av privat återställningsnyckel**  
      Ange hur ofta den privata återställningsnyckeln för en enhet ska roteras. Du kan välja standardinställningen **Inte konfigurerat** eller ett värde på **1** till **12** månader.
    - **Beskrivning av depositionsplats för privat återställningsnyckel**  
      Skriv ett kort meddelande till användaren som förklarar hur de kan hämta sin privata återställningsnyckel. Användaren ser den här texten på inloggningsskärmen vid uppmaningen att ange sin privata återställningsnyckel om lösenordet glöms bort.

  - **Antal gånger som ignorering tillåts**  
    Ange det antal gånger som användare kan ignorera frågor om att aktivera FileVault innan FileVault krävs för att de ska kunna logga in.
    - **Inte konfigurerad** (*standard*) – kryptering krävs på enheten innan nästa inloggning tillåts.
    - **1** till **10** – tillåt användare att ignorera uppmaningen från 1 till 10 gånger innan kryptering på enheten krävs.
    - **Ingen gräns, fråga alltid** – användaren uppmanas att aktivera FileVault, men kryptering är inte obligatorisk.

  - **Tillåt uppskjutning till utloggning**  
    - **Ej konfigurerat** (*standard*)
    - **Ja** – skjut upp uppmaningen att aktivera FileVault tills användaren loggar ut.  

  - **Inaktivera fråga vid utloggning**  
    Förhindra uppmaningen till användare att aktivera FileVault när de loggar ut. När det här anges till Inaktivera visas inget meddelande vid utloggning. I stället får användarna en uppmaning när de loggar in.
    - **Ej konfigurerat** (*standard*)
    - **Ja** – inaktivera uppmaningen att aktivera FileVault som visas vid utloggning.

  - **Dölj återställningsnyckel**  
     Dölj den personliga återställningsnyckeln från användaren av macOS-enheten vid kryptering. När disken är krypterad kan en användare använda valfri enhet till att visa sin personliga återställningsnyckel via Företagsportal-webbplatsen för Intune eller appen Företagsportal på en plattform som stöds.
    - **Ej konfigurerat** (*standard*)
    - **Ja** – Dölj den personliga återställningsnyckeln när enheten krypteras.

## <a name="bitlocker"></a>BitLocker

### <a name="bitlocker--base-settings"></a>BitLocker – grundläggande inställningar

- **Aktivera fullständig diskkryptering för operativsystem och fasta dataenheter**  
  CSP: [RequireDeviceEncryption](https://go.microsoft.com/fwlink/?linkid=872523)

  Om enheten krypterades innan den här principen tillämpades vidtas ingen extra åtgärd. Om krypteringsmetoden och alternativen stämmer överens med den här principen ska konfigurationen returnera lyckat resultat. Om ett alternativ för BitLocker-konfiguration på plats inte matchar den här principen kommer konfigurationen troligen att returnera ett fel.
  
  Om du vill tillämpa den här principen på en disk som redan är krypterad dekrypterar du enheten och tillämpar MDM-principen igen. Standardinställningen i Windows är att inte kräva diskkryptering med BitLocker. För Azure AD-anslutning och Microsoft Account (MSA)-registrering/-inloggning kan däremot automatisk kryptering tillämpa aktivering av BitLocker med XTS-AES 128-bitars kryptering.

  - **Inte konfigurerat** (*standard*) – ingen BitLocker-kryptering sker.
  - **Ja** – framtvinga användning av BitLocker.

- **Kräv att lagringskort ska krypteras (endast mobil)**  
  CSP: [RequireStorageCardEncryption](https://go.microsoft.com/fwlink/?linkid=872524)

  Den här inställningen gäller endast för Windows Mobile- och Mobile Enterprise SKU-enheter.
  - **Inte konfigurerat** (*standard*) – inställningen återgår till operativsystemets standardinställning som är att inte kräva kryptering på lagringskort.
  - **Ja** – kryptering på minneskort krävs för mobila enheter.

- **Dölj uppmaning om tredjepartskryptering**  
  CSP: [AllowWarningForOtherDiskEncryption](https://go.microsoft.com/fwlink/?linkid=872525)

  Om BitLocker är aktiverat på ett system som redan är krypterat med en krypteringsprodukt från tredje part kanske enheten inte kan användas. Du kan förlora data och behöva installera om Windows. Vi rekommenderar att du aldrig aktiverar BitLocker på en enhet där tredjepartskryptering är installerad eller aktiverad.

  Som standard uppmanas användare i installationsguiden för BitLocker att bekräfta att ingen tredjepartskryptering används.

  - **Inte konfigurerat** (*standard*) – installationsguiden för BitLocker visar en varning och användaren uppmanas att bekräfta att ingen tredjepartskryptering används.
  - **Ja** – dölj uppmaningar till användarna i installationsguiden för BitLocker.

  Om funktionerna för tyst aktivering av BitLocker är obligatoriska måste varningen om tredjepartskryptering vara dold eftersom alla obligatoriska uppmaningar bryter mot arbetsflödet för tyst aktivering.

  När värdet är *Ja* kan du sedan konfigurera följande inställning:

  - **Låt standardanvändare aktivera kryptering i Autopilot**  
    CSP: [AllowStandardUserEncryption](https://go.microsoft.com/fwlink/?linkid=2114200)
    - **Inte konfigurerat** (*standard*) – i scenarier med tyst aktivering av Azure Active Directory Join (AADJ) behöver inte användarna vara lokala administratörer för att aktivera BitLocker.
    - **Ja** – klientens standardinställning används, som är att kräva lokal administratörsbehörighet för att aktivera BitLocker.

    Användaren måste vara lokal administratör för att slutföra installationsguiden för BitLocker i scenarier utan tyst aktivering och med Autopilot.

- **Aktivera klientbaserad rotering av återställningslösenord**  
  CSP: [ConfigureRecoveryPasswordRotation](https://go.microsoft.com/fwlink/?linkid=2114201)

  Nyckelrotation stöds inte för AWA-enheter (Add Work Account, formellt Workplace Join).
  - **Inte konfigurerat** (*standard*) – klienten roterar inte återställningsnycklar för BitLocker.
  - **Inaktiverad**
  - **Azure AD-anslutna enheter**
  - **Azure AD- och hybridanslutna enheter**

### <a name="bitlocker---fixed-drive-settings"></a>BitLocker – inställningar för fasta enheter

- **Princip för BitLocker på fasta enheter**  
  [BitLocker-grupprincipinställningar](https://go.microsoft.com/fwlink/?linkid=2067018)

  - **Återställning av fast enhet**  
    CSP: [FixedDrivesRecoveryOptions](https://go.microsoft.com/fwlink/?linkid=872538)

    Styr hur fasta dataenheter som skyddas med BitLocker ska återställas om den nödvändiga startnyckelinformationen saknas.

    - **Inte konfigurerat** (*standard*) – standardalternativen för återställning används inklusive DRA (dataåterställningsagenten). Slutanvändaren kan ange återställningsalternativ och återställningsinformationen säkerhetskopieras inte till Azure Active Directory.
    - **Konfigurera** – aktivera åtkomst för att konfigurera olika metoder för återställning av enheter.

    Följande inställningar är tillgängliga när du anger *Konfigurera*:

    - **Återställningsnyckel skapad av användare**  
      - **Blockerat** (*standard*)
      - **Obligatoriskt**
      - **Tillåts**

    - **Konfigurera återställningspaket för BitLocker**
      - **Lösenord och nyckel** (*standard*) – inkludera både återställningslösenordet för BitLocker som administratörer och användare låser upp skyddade enheter med och återställningsnyckelpaket som administratörerer använder till dataåterställning i Active Directory.
      - **Endast lösenord** – återställningsnyckelpaketen kanske inte är tillgängliga vid behov.

    - **Kräv att enheten ska säkerhetskopiera återställningsinformation till Azure AD**
      - **Inte konfigurerat** (*standard*) – BitLocker-aktiveringen slutförs även om säkerhetskopieringen av återställningsnyckeln till Azure AD misslyckas. Det här kan leda till att ingen återställningsinformation lagras externt.
      - **Ja**- BitLocker slutför inte aktiveringen förrän återställningsnycklar har sparats i Azure Active Directory.

    - **Återställningslösenord skapat av användare**  
      - **Blockerat** (*standard*)
      - **Obligatoriskt**
      - **Tillåts**

    - **Dölj återställningsalternativ under installationen av BitLocker**
      - **Inte konfigurerat** (*standard*) – användaren har tillgång till extra återställningsalternativ.
      - **Ja** – hindra att slutanvändaren väljer extra återställningsalternativ, som att skriva ut återställningsnycklar i installationsguiden för BitLocker.

    - **Aktivera BitLocker när återställningsinformationen har lagrats**
      - **Ej konfigurerat** (*standard*)  
      - **Ja**

    - **Blockera användningen av certifikatbaserad dataåterställningsagent (DRA)**
      - **Inte konfigurerat** (*standard*) – tillåt användning av DRA. För att ställa in DRA krävs ett företags-PKI och ett grupprincipobjekt till att distribuera DRA-agenten och certifikaten.
      - **Ja** – blockera möjligheten att använda en dataåterställningsagent (DRA) till att återställa BitLocker-aktiverade enheter.

  - **Blockera skrivåtkomst till fasta dataenheter som inte skyddas av BitLocker**  
    CSP: [FixedDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872534)  
    Den här inställningen är tillgänglig när *Princip för BitLocker på fasta enheter* har angetts till *Konfigurera*.

    - **Inte konfigurerat** (*standard*) – Data kan skrivas till icke-krypterade fasta enheter.
    - **Ja** – Windows tillåter inte att data skrivs till fasta enheter som inte är BitLocker-skyddade. Om en fast enhet inte är krypterad måste användaren slutföra installationsguiden för BitLocker för enheten innan skrivåtkomst beviljas.

  - **Konfigurera krypteringsmetod för fasta dataenheter**  
    CSP: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  

    Konfigurera krypteringsmetod och krypteringsgrad för fasta dataenhetsdiskar. *XTS-AES 128-bitars* är Windows standardkrypteringsmetod och det rekommenderade värdet.

    - **Ej konfigurerat** (*standard*)
    - **AES 128-bitars CBC**
    - **AES 256-bitars CBC**
    - **AES 128-bitars XTS**
    - **AES 256-bitars XTS**

### <a name="bitlocker---os-drive-settings"></a>BitLocker – inställningar för operativsystemenheter

- **Princip för BitLocker på systemenheter**  
  CSP: [BitLocker-grupprincipinställningar](https://go.microsoft.com/fwlink/?linkid=2067025)

  - **Konfigurera** (*standard*)  
  - **Inte konfigurerat**

  När värdet är *Konfigurera* kan du konfigurera följande inställningar:

  - **Startautentisering krävs**  
    CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

    - **Ej konfigurerat** (*standard*)
    - **Ja** – konfigurera ytterligare autentiseringskrav vid systemstart, till exempel användning av betrodd plattformsmodul (TPM) eller PIN-kodskrav vid start.

    När värdet är *Ja* kan du konfigurera följande inställningar:

    - **Kompatibel TPM-start**  
      CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      Vi rekommenderar att du kräver en TPM för BitLocker. Den här inställningen gäller bara när du först aktiverar BitLocker och har inte någon effekt om BitLocker redan är aktiverat.

      - **Blockerat** (*standard*) – BitLocker använder inte TPM:en.
      - **Obligatoriskt** – BitLocker aktiveras bara om det finns en TPM som kan användas.
      - **Tillåtet** – BitLocker använder TPM:en om den finns.

    - **Kompatibel PIN-kod för TPM-start**  
      CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      - **Blockerat** (*standard*) – blockera användningen av en PIN-kod.
      - **Obligatoriskt** – PIN-kod och TPM måste användas för att aktivera BitLocker.
      - **Tillåtet** – BitLocker använder TPM:en om den finns och tillåter att användaren konfigurerar start med PIN-kod.

      I scenarier med tyst aktivering måste du ange *Blockerat*. Scenarier med tyst aktivering (inklusive Autopilot) lyckas inte när det krävs interaktion av användaren.

    - **Kompatibel nyckel för TPM-start**  
      CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      - **Blockerat** (*standard*) – blockera användningen av startnycklar.
      - **Obligatoriskt** – startnyckel och TPM måste användas för att aktivera BitLocker.
      - **Tillåtet** – BitLocker använder TPM:en om den finns och tillåter att en startnyckel (till exempel en USB-enhet) används för att låsa upp enheterna.

      I scenarier med tyst aktivering måste du ange *Blockerat*. Scenarier med tyst aktivering (inklusive Autopilot) lyckas inte när det krävs interaktion av användaren.

    - **Kompatibel nyckel och PIN-kod för TPM-start**  
      CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      - **Blockerat** (*standard*) – blockera användningen av kombinationen startnyckel och PIN-kod.
      - **Obligatoriskt**– BitLocker måste ha en startnyckel och PIN-kod tillgänglig för att aktiveras.
      - **Tillåtet** – BitLocker använder TPM:en om den finns och tillåter kombinationen med startnyckel och PIN-kod.

      I scenarier med tyst aktivering måste du ange *Blockerat*. Scenarier med tyst aktivering (inklusive Autopilot) lyckas inte när det krävs interaktion av användaren.

    - **Inaktivera BitLocker på enheter där TPM är inkompatibel**  
    CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      Om det inte finns någon TPM kräver BitLocker ett lösenord eller en USB-enhet för att starta.

      Den här inställningen gäller bara när du först aktiverar BitLocker och har inte någon effekt om BitLocker redan är aktiverat.

      - **Ej konfigurerat** (*standard*)
      - **Ja** – blockera att BitLocker konfigureras utan ett kompatibelt TPM-chip.

    - **Aktivera återställningsmeddelande och webbadress i förstartsmiljö**  
      CSP: [SystemDrivesRecoveryMessage](https://go.microsoft.com/fwlink/?linkid=872530)configure

      - **Inte konfigurerat** (*standard*) – använd standardinformationen om återställning före start i BitLocker.
      - **Ja** – aktivera konfiguration av ett anpassat återställningsmeddelande före start och en webbadress som hjälper användarna att förstå hur de kan hitta sina återställningslösenord. Användarna ser meddelandet före start och webbadressen när de är utelåsta från datorn i återställningsläge.

      När värdet är *Ja* kan du konfigurera följande inställningar:

      - **Återställningsmeddelande i förstartsmiljö**  
        Ange ett eget återställningsmeddelande före start.

      - **Återställningswebbadress i förstartsmiljö**  
        Ange en egen återställningsadress före start.

    - **Återställning av systemenhet**  
      CSP: [SystemDrivesRecoveryOptions](https://go.microsoft.com/fwlink/?linkid=872529)

      - **Ej konfigurerat** (*standard*)  
      - **Konfigurera** – aktivera konfigurationen av ytterligare inställningar.

      Följande inställningar är tillgängliga när du anger *Konfigurera*:

      - **Återställningsnyckel skapad av användare**  
        - **Blockerat** (*standard*)
        - **Obligatoriskt**
        - **Tillåts**

      - **Konfigurera återställningspaket för BitLocker**
        - **Lösenord och nyckel** (*standard*) – inkludera både återställningslösenordet för BitLocker som administratörer och användare låser upp skyddade enheter med och återställningsnyckelpaket som administratörerer använder till dataåterställning i Active Directory.
        - **Endast lösenord** – återställningsnyckelpaketen kanske inte är tillgängliga vid behov.

      - **Kräv att enheten ska säkerhetskopiera återställningsinformation till Azure AD**
        - **Inte konfigurerat** (*standard*) – BitLocker-aktiveringen slutförs även om säkerhetskopieringen av återställningsnyckeln till Azure AD misslyckas. Det här kan leda till att ingen återställningsinformation lagras externt.
        - **Ja**- BitLocker slutför inte aktiveringen förrän återställningsnycklar har sparats i Azure Active Directory.

      - **Återställningslösenord skapat av användare**  
        - **Blockerat** (*standard*)
        - **Obligatoriskt**
        - **Tillåts**

      - **Dölj återställningsalternativ under installationen av BitLocker**
        - **Inte konfigurerat** (*standard*) – användaren har tillgång till extra återställningsalternativ.
        - **Ja** – hindra att slutanvändaren väljer extra återställningsalternativ, som att skriva ut återställningsnycklar i installationsguiden för BitLocker.

      - **Aktivera BitLocker när återställningsinformationen har lagrats**
        - **Ej konfigurerat** (*standard*)  
        - **Ja**

      - **Blockera användningen av certifikatbaserad dataåterställningsagent (DRA)**
        - **Inte konfigurerat** (*standard*) – tillåt användning av DRA. För att ställa in DRA krävs ett företags-PKI och ett grupprincipobjekt till att distribuera DRA-agenten och certifikaten.
        - **Ja** – blockera möjligheten att använda en dataåterställningsagent (DRA) till att återställa BitLocker-aktiverade enheter.

    - **Minimilängd för PIN-kod**  
      CSP: [SystemDrivesMinimumPINLength](https://go.microsoft.com/fwlink/?linkid=872528)

      Ange minsta längd på start-PIN när TPM + PIN krävs för aktivering av BitLocker. PIN-koden måste vara mellan 4 och 20 siffror.

      Om du inte konfigurerar inställningen kan användarna konfigurera en PIN-kod för start med valfri längd (mellan 4 och 20 siffror)

      Den här inställningen gäller bara när du först aktiverar BitLocker och har inte någon effekt om BitLocker redan är aktiverat.

  - **Konfigurera krypteringsmetod för operativsystemenheter**  
   CSP: [EncryptionMethodByDriveType]( https://go.microsoft.com/fwlink/?linkid=872526)

    Konfigurera krypteringsmetod och krypteringsgrad för operativsystemenheter. *XTS-AES 128-bitars* är Windows standardkrypteringsmetod och det rekommenderade värdet.

    - **Ej konfigurerat** (*standard*)
    - **AES 128-bitars CBC**
    - **AES 256-bitars CBC**
    - **AES 128-bitars XTS**
    - **AES 256-bitars XTS**

### <a name="bitlocker---removable-drive-settings"></a>BitLocker – inställningar för flyttbara enheter

- **Konfigurera krypteringsmetod för operativsystemenheter**  
  CSP: [BitLocker-grupprincipinställningar](https://go.microsoft.com/fwlink/?linkid=2067140)

  - **Ej konfigurerat** (*standard*)  
  - **I**

  När värdet är *Konfigurera* kan du konfigurera följande inställningar.

  - **Konfigurera krypteringsmetod för flyttbara dataenheter**  
    CSP: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)

    Välj önskad krypteringsmetod för flyttbara datadiskenheter.

    - **Ej konfigurerat** (*standard*)
    - **AES 128-bitars CBC**
    - **AES 256-bitars CBC**
    - **AES 128-bitars XTS**
    - **AES 256-bitars XTS**

  - **Blockera skrivåtkomst till flyttbara dataenheter som inte skyddas av BitLocker**  
    CSP: [RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)

    - **Inte konfigurerat** (*standard*) – Data kan skrivas till icke-krypterade flyttbara enheter.
    - **Ja** – Windows tillåter inte att data skrivs till flyttbara enheter som inte skyddas med BitLocker. Om en ansluten flyttbar enhet inte är krypterad måste användaren slutföra installationsguiden för BitLocker innan skrivåtkomst beviljas.

    - **Blockera skrivåtkomst till flyttbara dataenheter som inte skyddas av BitLocker**  
      CSP: [RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)

      - **Inte konfigurerat** (*standard*) – alla BitLocker-krypterade enheter kan användas.
      - **Ja** – blockera åtkomst till flyttbara enheter om de inte har krypterats i en dator som ägs av organisationen.

## <a name="next-steps"></a>Nästa steg

[Endpoint Security-policyn Diskkryptering](../protect/endpoint-security-disk-encryption-policy.md)
