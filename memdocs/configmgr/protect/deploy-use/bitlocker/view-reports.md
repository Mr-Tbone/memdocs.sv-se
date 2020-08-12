---
title: Se BitLocker-rapporter
titleSuffix: Configuration Manager
description: Lär dig mer om hanterings rapporter i BitLocker i Configuration Manager
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: reference
ms.assetid: 0bae9477-0500-41cf-8aa3-5e6efadd0554
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7c44ec9a9ed91d8543fedbdd5fba191b3989da19
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129228"
---
# <a name="view-bitlocker-reports"></a>Se BitLocker-rapporter

*Gäller för: Configuration Manager (aktuell gren)*

<!--3601034-->

När du har [installerat rapporterna](setup-websites.md) på repor ting Services-platsen kan du visa rapporterna. I rapporterna visas kompatibilitet för BitLocker för företaget och för enskilda enheter. De tillhandahåller tabell information och diagram och har filter som gör att du kan visa data från olika perspektiv.

I Configuration Manager-konsolen går du till arbets ytan **övervakning** , expanderar **rapportering**och väljer noden **rapporter** . Följande rapporter finns i **hanterings** kategorin för BitLocker:

- [Kompatibilitet för BitLocker-dator](#bkmk-compliancereport)

- [Instrument panel för BitLocker Enterprise Compliance](#bkmk-dashboard)

- [Information om Enterprise-efterlevnad för BitLocker](#bkmk-compliancedetails)

- [Översikt över kompatibilitet för BitLocker Enterprise](#bkmk-compliancesummary)

- [Återställnings gransknings rapport](#bkmk-audit)

Du kan komma åt alla dessa rapporter direkt från webbplatsen repor ting Services-plats.

> [!NOTE]
> För att de här rapporterna ska visa fullständiga data:
>
> - Skapa och distribuera en hanterings princip för BitLocker till en enhets samling
> - Klienter i mål samlingen måste skicka maskin varu inventering

## <a name="bitlocker-computer-compliance"></a><a name="bkmk-compliancereport"></a>Kompatibilitet för BitLocker-dator

Använd den här rapporten om du vill samla in information som är unik för en dator. Den ger detaljerad krypterings information om operativ system enheten och eventuella fasta data enheter. Om du vill visa information om varje enhet expanderar du posten dator namn. Den anger också principen som används för varje enhets typ på datorn.

:::image type="content" source="media/bitlocker-computer-compliance.png" alt-text="Exempel skärm bild av rapporten om kompatibilitet för BitLocker-dator" lightbox="media/bitlocker-computer-compliance.png":::

Du kan också använda den här rapporten för att avgöra den senaste kända BitLocker-krypterings statusen för borttappade eller stulna datorer. Configuration Manager fastställer enhetens efterlevnad baserat på de BitLocker-principer som du distribuerar. Innan du försöker fastställa BitLocker-krypterings statusen för en enhet kontrollerar du de principer som du har distribuerat till den.

> [!NOTE]
> Den här rapporten visar inte krypterings status för flyttbara data volymer.

### <a name="computer-details"></a>Dator information

|Kolumn &nbsp; namn|Beskrivning|
|----------------|----|
|Datornamn|Användardefinierat DNS-datornamn.|
|Domännamn|Fullständigt kvalificerat domän namn för datorn.|
|Typ av dator|Typ av dator, giltiga typer är **icke-bärbara** och **bärbara**.|
|Operativsystem|Datorns OS-typ.|
|Övergripande kompatibilitet|Datorns övergripande status för BitLocker-kompatibilitet. Giltiga tillstånd är **kompatibla** och **icke-kompatibla**. [Status för efterlevnaden per enhet](#bkmk_volume) kan ange olika efterlevnadsprinciper. Det här fältet representerar dock detta kompatibilitetstillstånd från den angivna principen.|
|Kompatibilitet för operativ system|Kompatibilitetsstatus för operativ systemet på datorn. Giltiga tillstånd är **kompatibla** och **icke-kompatibla**.|
|Kompatibilitet för fast data enhet|Kompatibilitetsstatus för en fast data enhet på datorn. Giltiga tillstånd är **kompatibla** och **icke-kompatibla**.|
|Senaste uppdaterings datum|Datum och tid då datorn senast kontaktade servern för att rapportera kompatibilitetsstatus.|
|Undantag|Anger om användaren är undantagen eller icke-undantagen från BitLocker-principen.|
|Undantagen användare|Användaren som är undantagen från BitLocker-principen.|
|Undantags datum|Datum då undantaget beviljades.|
|Status information för efterlevnad|Fel-och status meddelanden om datorns kompatibilitetstillstånd från den angivna principen.|
|Krypterings grad för principen|Krypterings styrka som du har valt i hanterings principen för BitLocker.|
|Princip: operativ systemen het|Anger om kryptering krävs för operativ system enheten och lämplig skydds typ.|
|Princip: fast data enhet|Anger om kryptering krävs för den fasta data enheten.|
|Tillverkare|Dator tillverkarens namn som det visas i datorns BIOS.|
|Modell|Dator tillverkarenas modell namn som det visas i datorns BIOS.|
|Enhets användare|Kända användare på datorn.|

### <a name="computer-volume"></a><a name="bkmk_volume"></a>Dator volym

|Kolumn &nbsp; namn|Beskrivning|
|----------------|----|
|Enhetsbeteckning|Datorns enhets beteckning.|
|Enhetstyp|Typ av enhet. Giltiga värden är **operativ systemen het** och **fast data enhet**. Dessa poster är fysiska enheter snarare än logiska volymer.|
|Krypterings grad|Krypterings styrka som du valde under i hanterings principen för BitLocker.|
|Skydds typer|Typ av skydd som du har valt i principen för att kryptera enheten. Giltiga skydds typer för en OS-enhet är **TPM** eller **TPM + PIN-kod**. Giltig skydds typ för en fast data enhet är ett **lösen ord**.|
|Skydds status|Anger att datorn aktiverade skydds typen som anges i principen. Giltiga tillstånd är **på** eller **av**.|
|Krypterings tillstånd|Krypterings status för enheten. Giltiga tillstånd är **krypterade**, **inte krypterade**eller krypterade **.**|

## <a name="bitlocker-enterprise-compliance-dashboard"></a><a name="bkmk-dashboard"></a>Instrument panel för BitLocker Enterprise Compliance

Den här rapporten innehåller följande grafer som visar status för BitLocker-kompatibilitet i organisationen:

- Distribution av kompatibilitetsstatus

- Distribution med icke-kompatibla fel

- Distribution av kompatibilitetsstatus per enhets typ

:::image type="content" source="media/bitlocker-enterprise-compliance-dashboard.png" alt-text="Exempel skärm bild av instrument panelen för BitLocker Enterprise Compliance" lightbox="media/bitlocker-enterprise-compliance-dashboard.png":::

### <a name="compliance-status-distribution"></a>Distribution av kompatibilitetsstatus

Det här cirkel diagrammet visar kompatibilitetsstatus för datorer i organisationen. Den visar även procent andelen datorer med denna kompatibilitetsstatus, jämfört med det totala antalet datorer i den valda samlingen. Det faktiska antalet datorer med varje status visas också.

Cirkel diagrammet visar följande kompatibilitetsstatus:

- Kompatibel

- Icke-kompatibel

- Användar undantag

- Tillfälligt användar undantag

- Principen är inte tvingande

- Okänt. De här datorerna rapporterade ett status fel eller är en del av samlingen, men har aldrig rapporterat sin kompatibilitetsstatus. Bristen på status för efterlevnad kan uppstå om datorn är frånkopplad från organisationen.

### <a name="non-compliant---errors-distribution"></a>Distribution med icke-kompatibla fel

Det här cirkel diagrammet visar de kategorier av datorer i organisationen som inte är kompatibla med den BitLocker-diskkryptering principen. Det visar också antalet datorer i varje kategori. Rapporten beräknar varje procent andel från det totala antalet icke-kompatibla datorer i samlingen.

- Fördröjd kryptering av användare

- Det gick inte att hitta en kompatibel TPM

- Systempartitionen är inte tillgänglig eller tillräckligt stor

- TPM, synlig men inte initierad

- Princip konflikt

- Väntar på automatisk etablering för TPM

- Ett okänt fel har inträffat

- Ingen information. De här datorerna har inte installerat BitLocker-hanteringsservern eller också är den installerad men inte aktive rad. Till exempel fungerar inte tjänsten.

### <a name="compliance-status-distribution-by-drive-type"></a>Distribution av kompatibilitetsstatus per enhets typ

Det här stapeldiagrammet visar den aktuella status för BitLocker-kompatibilitet efter enhets typ. Statusarna är **kompatibla** och **icke-kompatibla**. Staplar visas för fasta data enheter och OS-enheter. Rapporten innehåller datorer utan en fast data enhet och visar bara ett värde i **operativ systemets enhets** fält. Diagrammet innehåller inte användare som har beviljats ett undantag från BitLocker-diskkryptering principen eller kategorin ingen policy.

## <a name="bitlocker-enterprise-compliance-details"></a><a name="bkmk-compliancedetails"></a>Information om Enterprise-efterlevnad för BitLocker

Den här rapporten visar information om den övergripande kompatibiliteten i BitLocker i organisationen för den samling datorer som du har distribuerat hanterings principen för BitLocker till.

:::image type="content" source="media/bitlocker-enterprise-compliance-details.png" alt-text="Exempel skärm bild av kompabilitet för BitLocker Enterprise" lightbox="media/bitlocker-enterprise-compliance-details.png":::

|Kolumnnamn|Beskrivning|
|--- |--- |
|Hanterade datorer|Antal datorer som du har distribuerat en hanterings princip för BitLocker till.|
|% Kompatibel|Procent andelen kompatibla datorer i organisationen.|
|% Icke-kompatibel|Procent andelen icke-kompatibla datorer i organisationen.|
|% Okänd efterlevnad|Procent andel datorer med ett kompatibilitetstillstånd som inte är känt.|
|% Undantag|Procent andel av datorerna som är undantagna från BitLocker-krypterings kravet.|
|% Icke-undantagen|Procent andel datorer som inte är undantagna från BitLocker-krypterings kravet.|
|Kompatibel|Antal kompatibla datorer i organisationen.|
|Icke-kompatibel|Antal icke-kompatibla datorer i organisationen.|
|Okänd efterlevnad|Antal datorer med ett kompatibilitetstillstånd som inte är känt.|
|Undantagna|Antal datorer som är undantagna från kraven på BitLocker-kryptering.|
|Icke-undantagen|Antal datorer som inte är undantagna från BitLocker-krypterings kravet.|

### <a name="computer-details"></a>Dator information

|Kolumnnamn|Beskrivning|
|--- |--- |
|Datornamn|Den hanterade enhetens DNS-datornamn.|
|Domännamn|Fullständigt kvalificerat domän namn för datorn.|
|efterlevnadsstatus|Datorns övergripande kompatibilitetsstatus. Giltiga tillstånd är **kompatibla** och **icke-kompatibla**.|
|Undantag|Anger om användaren är undantagen eller icke-undantagen från BitLocker-principen.|
|Enhets användare|Användare av enheten.|
|Status information för efterlevnad|Fel-och status meddelanden om datorns kompatibilitetstillstånd från den angivna principen.|
|Senaste kontakt|Datum och tid då datorn senast kontaktade servern för att rapportera kompatibilitetsstatus.|

## <a name="bitlocker-enterprise-compliance-summary"></a><a name="bkmk-compliancesummary"></a>Översikt över kompatibilitet för BitLocker Enterprise

Använd den här rapporten för att visa den övergripande kompatibiliteten för BitLocker i organisationen. Det visar även kompatibiliteten för enskilda datorer som du har distribuerat hanterings principen för BitLocker till.

:::image type="content" source="media/bitlocker-enterprise-compliance-summary.png" alt-text="Exempel skärm bild av översikt över kompatibilitet för BitLocker Enterprise" lightbox="media/bitlocker-enterprise-compliance-summary.png":::

|Kolumnnamn|Beskrivning|
|--- |--- |
|Hanterade datorer|Antal datorer som du hanterar med BitLocker-principen.|
|% Kompatibel|Procent andelen kompatibla datorer i din organisation.|
|% Icke-kompatibel|Procent andelen icke-kompatibla datorer i din organisation.|
|% Okänd efterlevnad|Procent andel datorer med ett kompatibilitetstillstånd som inte är känt.|
|% Undantag|Procent andel av datorerna som är undantagna från BitLocker-krypterings kravet.|
|% Icke-undantagen|Procent andel datorer som inte är undantagna från BitLocker-krypterings kravet.|
|Kompatibel|Antal kompatibla datorer i din organisation.|
|Icke-kompatibel|Antal icke-kompatibla datorer i din organisation.|
|Okänd efterlevnad|Antal datorer med ett kompatibilitetstillstånd som inte är känt.|
|Undantagna|Antal datorer som är undantagna från kraven på BitLocker-kryptering.|
|Icke-undantagen|Antal datorer som inte är undantagna från BitLocker-krypterings kravet.|

## <a name="recovery-audit-report"></a><a name="bkmk-audit"></a>Återställnings gransknings rapport

> [!NOTE]
> Från och med version 2002 är den här rapporten endast tillgänglig på [webbplatsen för administration och övervakning av BitLocker](helpdesk-portal.md#reports).<!-- 7629549 -->

Använd den här rapporten om du vill granska användare som har begärt åtkomst till återställnings nycklar för BitLocker. Du kan filtrera efter följande kriterier:

- En speciell typ av användare, till exempel en support användare eller en slutanvändare
- Om begäran misslyckades eller lyckades
- Den angivna typen av nyckel: lösen ord för återställnings nyckel, ID för återställnings nyckel eller hash för TPM-lösenord
- Ett datum intervall då hämtningen utfördes

:::image type="content" source="media/bitlocker-recovery-audit-report.png" alt-text="Exempel skärm bild av gransknings rapport för BitLocker-återställning" lightbox="media/bitlocker-recovery-audit-report.png":::

|Kolumn &nbsp; namn|Beskrivning|
|----------------|----|
|Datum och tid för begäran|Datum och tid då användaren begärde en nyckel för slutanvändaren eller supportavdelningen.|
|Källa för gransknings begär Anden|Den plats som begäran kom ifrån. Giltiga värden är **Självbetjäningsportal** eller **supportavdelningen**.|
|Resultat av begäran|Status för begäran. Giltiga värden har **lyckats** eller **misslyckats**.|
|Helpdesk-användare|Den administrativa användaren som begärde nyckeln. Om en helpdesk-administratör återställer nyckeln utan att ange användar namnet, är fältet **slutanvändare** tomt. En standard-helpdesk-användare måste ange användar namnet, som visas i det här fältet. För återställning via självbetjänings portalen visar det här fältet och fältet **slutanvändaren** namnet på användaren som gjorde begäran.|
|Slutanvändare|Namnet på den användare som begärde nyckel hämtning.|
|Dator|Namnet på den dator som återställdes.|
|Nyckeltyp|Typ av nyckel som användaren har begärt. De tre typerna av nycklar är:<br/><br/>- **Lösen ord för återställnings nyckel**: används för att återställa en dator i återställnings läge<br/>- **Återställnings nyckel-ID**: används för att återställa en dator i återställnings läge för en annan användare<br/>- **Hash för TPM-lösenord**: används för att återställa en dator med en låst TPM|
|Orsaks Beskrivning|Varför användaren begärde den angivna nyckel typen baserat på vilket alternativ de valt i formuläret.|
