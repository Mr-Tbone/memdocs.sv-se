---
title: Referens för BitLocker-inställningar
titleSuffix: Configuration Manager
description: Alla inställningar för BitLocker-hantering som är tillgängliga i Configuration Manager
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f7ade768-2b2b-4aab-8ee1-73624d03a9c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9ce6a9c566fec22e69c0a4a7fde01b911330ec1d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723931"
---
# <a name="bitlocker-settings-reference"></a>Referens för BitLocker-inställningar

*Gäller för: Configuration Manager (aktuell gren)*

<!-- 5925683 -->

Hanterings principer för BitLocker i Configuration Manager innehåller följande princip grupper:

- Installation
- Operativ system enhet
- Fast enhet
- Flyttbar enhet
- Klienthantering

I följande avsnitt beskrivs och föreslås konfigurationer för inställningarna i varje grupp.

> [!NOTE]
> De här inställningarna baseras på Configuration Manager version 2002. Version 1910 innehåller inte alla dessa inställningar.

## <a name="setup"></a>Installation

Inställningarna på den här sidan konfigurerar globala BitLocker-krypterings alternativ.

### <a name="drive-encryption-method-and-cipher-strength"></a>Enhets krypterings metod och krypterings grad

*Föreslagen konfiguration*: **aktive rad** med standard eller större krypterings metod.

> [!NOTE]
> Sidan **installations** egenskaper innehåller två inställnings grupper för olika versioner av Windows. I det här avsnittet beskrivs båda.

#### <a name="windows-81-devices"></a>Windows 8.1-datorer

För Windows 8,1-enheter aktiverar du alternativet för **enhets krypterings metod och**krypterings styrka och väljer någon av följande krypterings metoder:

- AES 128-bit med diffuser
- AES 256-bit med diffuser
- AES 128-bit (standard)
- AES 256-bit

#### <a name="windows-10-devices"></a>Windows 10-enheter

För Windows 10-enheter aktiverar du alternativet för **enhets krypterings metod och krypterings styrka (Windows 10)**. Välj individuellt en av följande krypterings metoder för OS-enheter, fasta data enheter och flyttbara data enheter:

- AES-CBC 128-bit
- AES-CBC 256-bit
- XTS-AES 128-bit (standard)
- XTS-AES 256-bit

> [!TIP]
> BitLocker använder avancerad krypteringsstandard (AES) som krypteringsalgoritm med konfigurerbar nyckllängd på 128 eller 256 bitar. På Windows 10-enheter stöder AES-krypteringen CBC (cipher block chainion) eller chiffertexten stjäla (XTS).
>
> Om du behöver använda en flyttbar enhet på enheter som inte kör Windows 10 använder du AES-CBC.

#### <a name="general-usage-notes-for-drive-encryption-and-cipher-strength"></a>Allmän användnings information för enhets kryptering och krypterings grad

- Om du inaktiverar eller inte konfigurerar de här inställningarna använder BitLocker standard krypterings metoden.

- Configuration Manager tillämpar dessa inställningar när du aktiverar BitLocker.

- Om enheten redan är krypterad eller pågår ändras inte enhetens kryptering på enheten.

- Om du använder standardvärdet kan det hända att rapporten för BitLocker-datorns efterlevnad visar krypterings styrkan som **okänd**. Du kan lösa problemet genom att aktivera den här inställningen och ange ett explicit värde för krypterings styrka.

### <a name="prevent-memory-overwrite-on-restart"></a>Förhindra överskrivning av minne vid omstart

*Föreslagen konfiguration*: **inte konfigurerad**

Konfigurera den här principen för att förbättra start prestanda utan att skriva över BitLocker-hemligheter i minnet vid omstart.

När du inte konfigurerar den här principen, tar BitLocker bort dess hemligheter från minnet när datorn startas om.

### <a name="validate-smart-card-certificate-usage-rule-compliance"></a>Verifiera efterlevnad av certifikat användnings regel för smartkort

*Föreslagen konfiguration*: **inte konfigurerad**

Konfigurera den här principen för att använda smartkortscertifikat-baserat BitLocker-skydd. Ange sedan certifikat **objekts identifieraren**.

När du inte konfigurerar den här principen använder BitLocker standard objekt identifieraren `1.3.6.1.4.1.311.67.1.1` för att ange ett certifikat.

### <a name="organization-unique-identifiers"></a>Organisationens unika identifierare

*Föreslagen konfiguration*: **inte konfigurerad**

Konfigurera den här principen så att den använder en certifikatbaserad data återställnings agent eller BitLocker To Go-läsaren.

När du inte konfigurerar den här principen används inte **identifierings** fältet i BitLocker.

Om din organisation kräver högre säkerhets mått konfigurerar du fältet **identifiering** . Ange det här fältet på alla mål-USB-enheter och justera det med den här inställningen.

## <a name="os-drive"></a>OS-enhet

Inställningarna på den här sidan konfigurerar krypterings inställningarna för den enhet där Windows är installerat.

### <a name="operating-system-drive-encryption-settings"></a>Krypterings inställningar för operativ system enhet

*Föreslagen konfiguration*: **aktive rad**

Om du aktiverar den här inställningen måste användaren skydda operativ system enheten och BitLocker krypterar enheten. Om du inaktiverar den kan användaren inte skydda enheten. Om du inte konfigurerar den här principen krävs inte BitLocker-skydd på operativ system enheten.

> [!NOTE]
> Om enheten redan är krypterad och du inaktiverar den här inställningen dekrypterar BitLocker enheten.  

Om du har enheter utan en [Trusted Platform Module (TPM)](https://docs.microsoft.com/windows/security/information-protection/tpm/trusted-platform-module-top-node)använder du alternativet för att **tillåta BitLocker utan en kompatibel TPM (kräver ett lösen ord)**. Med den här inställningen kan BitLocker kryptera operativ system enheten, även om enheten inte har någon TPM. Om du tillåter det här alternativet, så begär Windows användaren att ange ett BitLocker-lösenord.

På enheter med en kompatibel TPM kan två typer av autentiseringsmetoder användas vid start för att ge extra skydd för krypterade data. När datorn startas kan den endast använda TPM: en för autentisering, eller så kan du också kräva att en PIN-kod tas med på en personlig kod. Konfigurera följande inställningar:

- **Välj skydd för operativ system enhet**: Konfigurera den att använda en TPM och PIN-kod eller bara TPM.

- **Konfigurera minimilängd för PIN-kod för start**: om du behöver en PIN-kod är det här värdet den kortaste längd som användaren kan ange. Användaren anger denna PIN-kod när datorn startar för att låsa upp enheten. Som standard är `4`minimilängd för PIN-kod.

> [!TIP]
> Om du vill ha högre säkerhet bör du *inaktivera* följande grup princip inställningar i**ström spar läge**för **systemets** > **energi** > spar läge när du aktiverar enheter med TPM + PIN-skydd:
>
> - Tillåt vänte lägen (S1-S3) vid ström spar läge (nätdrift)
>
> - Tillåt vänte lägen (S1-S3) vid ström spar läge (batteri drift)

### <a name="allow-enhanced-pins-for-startup"></a>Tillåt utökade PIN-instruktioner för start

*Föreslagen konfiguration*: **inte konfigurerad**

Konfigurera BitLocker för att använda förbättrade start-PIN-filer. Dessa PIN-märken tillåter användning av ytterligare tecken, till exempel versaler och gemener, symboler, siffror och blank steg. Den här inställningen gäller när du aktiverar BitLocker.

> [!IMPORTANT]
> Alla datorer har inte stöd för utökade PIN-adresser i för start miljön. Innan du aktiverar användningen ska du utvärdera om enheterna är kompatibla med den här funktionen.

Om du aktiverar den här inställningen tillåter alla nya start-pinn av BitLocker att användaren skapar utökade PIN-filer.

- **Kräv endast ASCII-PIN-** kod: hjälp till att göra förbättrade PIN-bara kompatibla med datorer som begränsar typen eller antalet tecken som du kan ange i Pre-Boot-miljön.

Om du inaktiverar eller inte konfigurerar den här policy inställningen använder BitLocker inte utökade PIN-regler.

### <a name="operating-system-drive-password-policy"></a>Lösen ords princip för operativ Systems enhet

*Föreslagen konfiguration*: **inte konfigurerad**

Använd de här inställningarna för att ange begränsningar för lösen ord för att låsa upp BitLocker-skyddade OS-enheter. Om du tillåter icke-TPM-skydd på OS-enheter konfigurerar du följande inställningar:

- **Konfigurera lösen ords komplexitet för operativ system enheter**: om du vill framtvinga komplexitets krav på lösen ordet väljer du **Kräv lösen ords komplexitet**.

- **Minsta längd på lösen ord för operativ systemen het**: den minsta längden är `8`som standard.

- **Kräv endast ASCII-lösenord för flyttbara OS-enheter**

Om du aktiverar den här inställningen kan användarna konfigurera ett lösen ord som uppfyller de krav som du definierar.

#### <a name="general-usage-notes-for-os-drive-password-policy"></a>Allmän användnings information för lösen ords princip för operativ system enhet

- För att de här komplexitets kraven ska vara effektiva måste du också aktivera grup princip inställningen **lösen ord måste uppfylla komplexitets kraven** i **dator konfiguration** > **Windows-inställningar** > **säkerhets inställningar** > **konto principer** > **lösen ords princip**.

- BitLocker tillämpar dessa inställningar när du aktiverar den, inte när du låser upp en volym. Med BitLocker kan du låsa upp en enhet med någon av de skydds enheter som är tillgängliga på enheten.

- Om du använder grup princip för att aktivera FIPS-kompatibla algoritmer för kryptering, hashing och signering kan du inte tillåta lösen ord som BitLocker-skydd.

### <a name="reset-platform-validation-data-after-bitlocker-recovery"></a>Återställ plattforms verifierings data efter BitLocker-återställning

*Föreslagen konfiguration*: **inte konfigurerad**

Kontrol lera om Windows uppdaterar plattforms verifierings data när den startas efter BitLocker-återställning.

Om du aktiverar eller inte konfigurerar den här inställningen uppdaterar Windows plattforms verifierings data i den här situationen.

Om du inaktiverar den här inställningen uppdaterar Windows inte plattforms validerings data i den här situationen.

### <a name="pre-boot-recovery-message-and-url"></a>Återställningsmeddelande och webbadress i förstartsmiljö

*Föreslagen konfiguration*: **inte konfigurerad**

När BitLocker låser operativ system enheten använder du den här inställningen för att visa ett anpassat återställnings meddelande eller en URL på skärmen för BitLocker-återställning före start. Den här inställningen gäller endast för Windows 10-enheter.

När du aktiverar den här inställningen väljer du något av följande alternativ för återställnings meddelandet för för start:

- **Använd standard återställnings meddelande och webb adress**: Visa standard återställnings meddelande och URL för BitLocker i start sidan för BitLocker-återställning. Om du tidigare har konfigurerat ett anpassat återställnings meddelande eller en URL använder du det här alternativet för att återgå till standard meddelandet.

- **Använd anpassat återställnings meddelande**: inkludera ett anpassat meddelande i start sidan för BitLocker-återställning.

  - **Anpassat återställnings meddelande alternativ**: Ange det anpassade meddelande som ska visas. Om du också vill ange en återställnings-URL inkluderar du den som en del av det här anpassade återställnings meddelandet. Den maximala sträng längden är 32 768 tecken.

- **Använd anpassad återställnings-URL**: Ersätt standard-URL: en som visas på skärmen för BitLocker-återställning före start.

  - **Alternativ för anpassad återställnings webb adress**: Ange den URL som ska visas. Den maximala sträng längden är 32 768 tecken.

> [!NOTE]
> Det finns inte stöd för alla tecken och språk i för start. Testa det anpassade meddelandet eller URL: en för att kontrol lera att det visas korrekt på skärmen för BitLocker-återställning före start.

### <a name="encryption-policy-enforcement-settings-os-drive"></a>Tvingande inställningar för krypterings princip (OS-enhet)

*Föreslagen konfiguration*: **aktive rad**

Konfigurera antalet dagar som användare kan skjuta upp BitLocker-kompatibiliteten för operativ system enheten. **Grace-perioden för inkompatibilitet** börjar när Configuration Manager först identifierar den som inkompatibel. När den här Grace-perioden går ut kan användarna inte skjuta upp den nödvändiga åtgärden eller begära ett undantag.

Om krypterings processen kräver indata från användaren visas en dialog ruta i Windows som användaren inte kan stänga förrän de anger den information som krävs. Framtida meddelanden om fel eller status har inte den här begränsningen.

Om BitLocker inte kräver användar interaktion för att lägga till en skydds tid, efter det att respittiden har gått ut, startar BitLocker kryptering i bakgrunden.

Om du inaktiverar eller inte konfigurerar den här inställningen kräver Configuration Manager inte att användare följer BitLocker-principer.

Om du vill genomdriva principen omedelbart ställer du in en `0`respitperiod på.

## <a name="fixed-drive"></a>Fast enhet

Inställningarna på den här sidan konfigurerar kryptering för ytterligare data enheter i en enhet.

### <a name="fixed-data-drive-encryption"></a>Fast data enhets kryptering

*Föreslagen konfiguration*: **aktive rad**

Hantera ditt krav för kryptering av fasta data enheter. Om du aktiverar den här inställningen kräver BitLocker att användare lägger till alla fasta data enheter under skyddet. Sedan krypteras data enheterna.

När du aktiverar den här principen aktiverar du antingen automatisk upplåsning eller inställningarna för **lösen ords princip för fast data enhet**.

- **Konfigurera automatisk upplåsning för fast data enhet**: Tillåt eller Kräv att BitLocker automatiskt låser upp en krypterad data enhet. Om du vill använda automatisk upplåsning måste du också använda BitLocker för att kryptera [operativ system enheten](#os-drive).

Om du inte konfigurerar den här inställningen kräver inte BitLocker användare att lägga till fasta data enheter under skyddet.

Om du inaktiverar den här inställningen kan användarna inte sätta sina fasta data enheter under BitLocker-skydd. Om du inaktiverar den här principen när BitLocker krypterar fasta data enheter dekrypterar BitLocker de fasta data enheterna.

### <a name="deny-write-access-to-fixed-drives-not-protected-by-bitlocker"></a>Neka skriv åtkomst till fasta enheter som inte skyddas av BitLocker

*Föreslagen konfiguration*: **inte konfigurerad**

Kräv att BitLocker-skyddet för Windows ska skriva data till fasta enheter på enheten. Den här principen tillämpas i BitLocker när du aktiverar den.

När du aktiverar den här inställningen:

- Om BitLocker skyddar en fast data enhet, monterar Windows den med Läs-och skriv åtkomst.

- För en fast data enhet som BitLocker inte skyddar monteras den som skrivskyddad.

När du inte konfigurerar den här inställningen monterar Windows alla fasta data enheter med Läs-och skriv åtkomst.

<!-- ### Allow access to BitLocker-protected fixed drives from earlier versions of Windows -->

### <a name="fixed-data-drive-password-policy"></a>Lösen ords princip för fast data enhet

*Föreslagen konfiguration*: **inte konfigurerad**

Använd de här inställningarna för att ange begränsningar för lösen ord för att låsa upp BitLocker-skyddade fasta data enheter.

Om du aktiverar den här inställningen kan användarna konfigurera ett lösen ord som uppfyller dina definierade krav.

För högre säkerhet aktiverar du den här inställningen och konfigurerar sedan följande inställningar:

- **Kräv lösen ord för fast data enhet**: användare måste ange ett lösen ord för att låsa upp en BitLocker-skyddad fast data enhet.

- **Konfigurera lösen ords komplexitet för fasta data enheter**: om du vill framtvinga komplexitets krav på lösen ordet väljer du **Kräv lösen ords komplexitet**.

- **Minsta längd på lösen ord för fast data enhet**: den minsta längden är `8`som standard.

Om du inaktiverar den här inställningen kan användarna inte konfigurera ett lösen ord.

När principen inte har kon figurer ATS stöder BitLocker lösen ord med standardinställningarna. Standardinställningarna omfattar inte komplexitets kraven för lösen ord och kräver bara åtta tecken.

#### <a name="general-usage-notes-for-fixed-data-drive-password-policy"></a>Allmän användnings information för lösen ords princip för fast data enhet

- För att de här komplexitets kraven ska vara effektiva måste du också aktivera grup princip inställningen **lösen ord måste uppfylla komplexitets kraven** i **dator konfiguration** > **Windows-inställningar** > **säkerhets inställningar** > **konto principer** > **lösen ords princip**.

- BitLocker tillämpar dessa inställningar när du aktiverar den, inte när du låser upp en volym. Med BitLocker kan du låsa upp en enhet med någon av de skydds enheter som är tillgängliga på enheten.

- Om du använder grup princip för att aktivera FIPS-kompatibla algoritmer för kryptering, hashing och signering kan du inte tillåta lösen ord som BitLocker-skydd.

### <a name="encryption-policy-enforcement-settings-fixed-data-drive"></a>Tvingande inställningar för krypterings princip (fast data enhet)

*Föreslagen konfiguration*: **aktive rad**

Konfigurera antalet dagar som användare kan skjuta upp BitLocker-kompatibilitet för fasta data enheter. **Grace-perioden för inkompatibilitet** börjar när Configuration Manager först identifierar den fasta data enheten som inkompatibel. Den fasta data enhets principen upprätthålls inte förrän operativ system enheten är kompatibel. När Grace-perioden har löpt ut kan användarna inte skjuta upp den nödvändiga åtgärden eller begära ett undantag.

Om krypterings processen kräver indata från användaren visas en dialog ruta i Windows som användaren inte kan stänga förrän de anger den information som krävs. Framtida meddelanden om fel eller status har inte den här begränsningen.

Om BitLocker inte kräver användar interaktion för att lägga till en skydds tid, efter det att respittiden har gått ut, startar BitLocker kryptering i bakgrunden.

Om du inaktiverar eller inte konfigurerar den här inställningen kräver Configuration Manager inte att användare följer BitLocker-principer.

Om du vill genomdriva principen omedelbart ställer du in en `0`respitperiod på.

## <a name="removable-drive"></a>Flyttbar enhet

Inställningarna på den här sidan konfigurerar kryptering för flyttbara enheter, till exempel USB-nycklar.

### <a name="removable-data-drive-encryption"></a>Kryptering av flyttbara data enheter

*Föreslagen konfiguration*: **aktive rad**

Den här inställningen styr användningen av BitLocker på flyttbara enheter.

- **Tillåt att användare använder BitLocker-skydd på flyttbara data enheter**: användare kan aktivera BitLocker-skyddet för en flyttbar enhet.

- **Tillåt att användare inaktiverar och dekrypterar BitLocker på flyttbara data enheter**: användare kan ta bort eller tillfälligt inaktivera BitLocker-diskkryptering från en flyttbar enhet.

När du aktiverar den här inställningen och låter användare använda BitLocker-skyddet sparar Configuration Manager-klienten återställnings information om flyttbara enheter till återställnings tjänsten på hanterings platsen. Med det här beteendet kan användare återställa enheten om de glömmer bort eller förlorar skydds inställningen (lösen ordet).

När du aktiverar den här inställningen:

- Aktivera inställningarna för **lösen ords princip för flyttbara data enheter**

- *Inaktivera* följande grup princip inställningar i **systemet** > **flyttbara lagrings utrymme** för både användare & datorkonfigurationer:

  - **Alla klasser för flyttbara lagringsmedia: neka all åtkomst**
  - **Flyttbara diskar: neka skriv åtkomst**
  - **Flyttbara diskar: neka Läs åtkomst**

Om du inaktiverar den här inställningen kan användarna inte använda BitLocker på flyttbara enheter.

### <a name="deny-write-access-to-removable-drives-not-protected-by-bitlocker"></a>Neka skriv åtkomst till flyttbara enheter som inte skyddas av BitLocker

*Föreslagen konfiguration*: **inte konfigurerad**

Kräv att BitLocker-skyddet för Windows ska skriva data till flyttbara enheter på enheten. Den här principen tillämpas i BitLocker när du aktiverar den.

När du aktiverar den här inställningen:

- Om BitLocker skyddar en flyttbar enhet monterar Windows den med Läs-och skriv åtkomst.

- För en flyttbar enhet som BitLocker inte skyddar monteras den som skrivskyddad.

- Om du aktiverar alternativet för att **neka skriv åtkomst till enheter som kon figurer ATS i en annan organisation**ger BitLocker bara skriv åtkomst till flyttbara enheter med identifierings fält som matchar de tillåtna identifierings fälten. Definiera de här fälten med **organisationens unika identifierare** globala inställningar på [installations](#setup) sidan.

När du inaktiverar eller inte konfigurerar den här inställningen monterar Windows alla flyttbara enheter med Läs-och skriv åtkomst.

> [!NOTE]
> Du kan åsidosätta den här inställningen med grup princip inställningar i **systemets** > **flyttbara lagrings åtkomst**. Om du aktiverar grup princip inställningen **flyttbara diskar: neka skriv åtkomst**ignorerar BitLocker den här Configuration Manager inställningen.

<!-- ### Allow access to BitLocker-protected removable data drives from earlier versions of Windows -->

### <a name="removable-data-drive-password-policy"></a>Lösen ords princip för flyttbara data enheter

*Föreslagen konfiguration*: **aktive rad**

Använd de här inställningarna för att ange begränsningar för lösen ord för att låsa upp BitLocker-skyddade flyttbara enheter.

Om du aktiverar den här inställningen kan användarna konfigurera ett lösen ord som uppfyller dina definierade krav.

För högre säkerhet aktiverar du den här inställningen och konfigurerar sedan följande inställningar:

- **Kräv lösen ord för flyttbar data enhet**: användare måste ange ett lösen ord för att låsa upp en BitLocker-skyddad flyttbar enhet.

- **Konfigurera lösen ords komplexitet för flyttbara data enheter**: om du vill framtvinga komplexitets krav på lösen ordet väljer du **Kräv lösen ords komplexitet**.

- **Minsta längd på lösen ord för flyttbar data enhet**: som standard är `8`den minimala längden.

Om du inaktiverar den här inställningen kan användarna inte konfigurera ett lösen ord.

När principen inte har kon figurer ATS stöder BitLocker lösen ord med standardinställningarna. Standardinställningarna omfattar inte komplexitets kraven för lösen ord och kräver bara åtta tecken.

#### <a name="general-usage-notes-for-removable-data-drive-password-policy"></a>Allmän användnings information för lösen ords princip för flyttbara data enheter

- För att de här komplexitets kraven ska vara effektiva måste du också aktivera grup princip inställningen **lösen ord måste uppfylla komplexitets kraven** i **dator konfiguration** > **Windows-inställningar** > **säkerhets inställningar** > **konto principer** > **lösen ords princip**.

- BitLocker tillämpar dessa inställningar när du aktiverar den, inte när du låser upp en volym. Med BitLocker kan du låsa upp en enhet med någon av de skydds enheter som är tillgängliga på enheten.

- Om du använder grup princip för att aktivera FIPS-kompatibla algoritmer för kryptering, hashing och signering kan du inte tillåta lösen ord som BitLocker-skydd.

## <a name="client-management"></a>Klienthantering

Inställningarna på den här sidan konfigurerar BitLocker-hanterings tjänster och-klienter.

### <a name="bitlocker-management-services"></a>Hanterings tjänster för BitLocker

*Föreslagen konfiguration*: **aktive rad**

När du aktiverar den här inställningen Configuration Manager automatisk och tyst säkerhets kopiering av nyckel återställnings information i plats databasen. Om du inaktiverar eller inte konfigurerar den här inställningen sparar Configuration Manager inte nyckel återställnings information.

- **Välj BitLocker-återställningsinformation som ska lagras**: Konfigurera nyckel återställnings tjänsten för att säkerhetskopiera BitLocker-återställningsinformation. Det ger en administrativ metod för att återskapa data som krypterats av BitLocker, vilket bidrar till att förhindra data förlust på grund av brist på viktig information.

- **Tillåt att återställnings information lagras i oformaterad text**: utan ett BitLocker-Management-signeringscertifikat för SQL Server Configuration Manager lagrar nyckel återställnings informationen i klartext. Mer information finns i [kryptera återställnings data](../../deploy-use/bitlocker/encrypt-recovery-data.md).

- **Status frekvens för klient kontroll (minuter)**: vid den konfigurerade frekvensen kontrollerar klienten BitLocker-skyddets principer och status på datorn och säkerhetskopierar även klient återställnings nyckeln. Som standard uppdaterar den Configuration Manager klienten sin BitLocker-återställningsinformation var 90: e minut.

### <a name="user-exemption-policy"></a>Princip för användar undantag

*Föreslagen konfiguration*: **inte konfigurerad**

Konfigurera en kontakt metod för användarna att begära ett undantag från BitLocker-kryptering.

Om du aktiverar den här inställningen anger du följande information:

- **Maximalt antal dagar att skjuta upp**: hur många dagar användaren kan skjuta upp en Tvingad princip. Som standard är `7` det här värdet dagar (en vecka).

- **Kontakt metod**: Ange hur användare kan begära undantag: URL, e-postadress eller telefonnummer.

- **Kontakt**: Ange URL, e-postadress eller telefonnummer. När en användare begär ett undantag från BitLocker-skyddet visas en dialog ruta i Windows med instruktioner om hur du använder. Configuration Manager verifierar inte den information du anger.

  - **URL**: Använd standard-URL- `https://website.domain.tld`formatet. Windows visar URL: en som en hyperlänk.

  - **E-post adress**: Använd standardformat för `user@domain.tld`e-postadress. Windows visar adressen som följande hyperlänk: `mailto:user@domain.tld?subject=Request exemption from BitLocker protection`.

  - **Telefonnummer**: Ange det nummer som du vill att användarna ska anropa. Windows visar talet med följande beskrivning: `Please call <your number> for applying exemption`.

Om du inaktiverar eller inte konfigurerar den här inställningen visas inte instruktionerna för undantags begär anden till användare i Windows.

> [!NOTE]
> BitLocker hanterar undantag per användare, inte per dator. Om flera användare loggar in på samma dator och en användare inte är undantagen krypteras datorn av BitLocker.

### <a name="url-for-the-security-policy-link"></a>URL för säkerhets princip länken

*Föreslagen konfiguration*: **aktive rad**

Ange en URL som ska visas för användarna som **företagets säkerhets princip** i Windows. Använd den här länken för att ge användare information om krypterings krav. Det visar när BitLocker efterfrågar användaren att kryptera en enhet.

Om du aktiverar den här inställningen konfigurerar du **URL för säkerhets princip länken**.

Om du inaktiverar eller inte konfigurerar den här inställningen visas inte länken säkerhets princip i BitLocker.
