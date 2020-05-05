---
title: Planera för BitLocker-hantering
titleSuffix: Configuration Manager
description: Planera för att hantera BitLocker-diskkryptering med Configuration Manager
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a4d8cda2-bc9b-4fb4-aa0d-23c31b4fc60b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 926d1483739b85f787ebc9e2a992ea7ed39633c2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722216"
---
# <a name="plan-for-bitlocker-management"></a>Planera för BitLocker-hantering

*Gäller för: Configuration Manager (aktuell gren)*

<!-- 3601034 -->

Från och med version 1910 använder Configuration Manager för att hantera BitLocker-diskkryptering (BDE) för lokala Windows-klienter. Den ger fullständig livs cykel hantering i BitLocker som kan ersätta användningen av Microsoft BitLocker administration and Monitoring (MBAM).

> [!Note]  
> Configuration Manager aktiverar inte den här valfria funktionen som standard. Du måste aktivera den här funktionen innan du använder den. Mer information finns i avsnittet [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).  

Mer information finns i [Översikt över BitLocker](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-overview).

> [!TIP]
> Om du vill hantera kryptering på samhanterade Windows 10-enheter med hjälp av moln tjänsten i Microsoft Endpoint Manager byter du [ **Endpoint Protection** arbets belastning](../../comanage/workloads.md#endpoint-protection) till Intune. Mer information om hur du använder Intune finns i [Windows-kryptering](/intune/protect/endpoint-protection-windows-10#windows-encryption).

## <a name="features"></a>Funktioner

Configuration Manager tillhandahåller följande hanterings funktioner för BitLocker-diskkryptering:

### <a name="client-deployment"></a>Klientdistribution

Distribuera BitLocker-klienten till hanterade Windows-enheter som kör Windows 10 eller Windows 8,1

### <a name="manage-encryption-policies"></a>Hantera krypterings principer

- Exempel: Välj enhets kryptering och krypterings styrka, konfigurera användar undantags princip, inställningar för fast data enhets kryptering.

- Bestäm vilka algoritmer som enheten ska krypteras med och de diskar som du är mål för kryptering.

- Tvinga användare att bli kompatibla med nya säkerhets principer innan du använder enheten.

- Anpassa din organisations säkerhets profil per enhet.

- När en användare låser upp operativ system enheten anger du om du vill låsa upp endast en operativ system enhet eller alla anslutna enheter.

### <a name="compliance-reports"></a>Rapporter om efterlevnad

Inbyggda rapporter för:

- Krypterings status per volym eller per enhet
- Enhetens primära användare
- Kompatibilitetsstatus
- Orsaker till bristande efterlevnad

### <a name="administration-and-monitoring-website"></a>Webbplats för administration och övervakning

Tillåt andra personer i din organisation utanför Configuration Manager-konsolen för att hjälpa till med nyckel återställning, inklusive nyckel rotation och annan BitLocker-relaterad support. Support administratörer kan till exempel hjälpa användare med nyckel återställning.

### <a name="user-self-service-portal"></a>Självbetjänings Portal för användare

Låt användarna hjälpa sig att använda en enda nyckel för att låsa upp en BitLocker-krypterad enhet. När den här nyckeln används skapas en ny nyckel för enheten.

## <a name="prerequisites"></a>Krav

- Om du vill skapa en princip för BitLocker-hantering behöver du rollen **Fullständig administratör** i Configuration Manager.

- BitLocker-återställningsnyckeln kräver HTTPS för att kryptera återställnings nycklarna över nätverket från konfigurationen hantera klienten till hanterings platsen. Det finns två alternativ:

  - HTTPS – Aktivera IIS-webbplatsen på hanterings platsen som är värd för återställnings tjänsten. Det här alternativet gäller endast för Configuration Manager version 2002.<!-- 5925660 -->

  - Konfigurera hanterings platsen för HTTPS. Det här alternativet gäller för Configuration Manager version 1910 eller 2002.

  Mer information finns i [kryptera återställnings data](../deploy-use/bitlocker/encrypt-recovery-data.md).

- Installera repor ting Services-platsens plats system roll om du vill använda BitLocker-hanterings rapporter. Mer information finns i [Konfigurera rapportering](../../core/servers/manage/configuring-reporting.md).

    > [!NOTE]
    > För att **rapporten återställnings granskning** ska fungera från webbplatsen för administration och övervakning använder du endast en repor ting Services-plats på den primära platsen.

- Om du vill använda självbetjänings portalen eller webbplatsen för administration och övervakning behöver du en Windows Server som kör IIS. Du kan återanvända ett Configuration Manager plats system eller använda en fristående webb server som har anslutning till plats databas servern. Använd en [OS-version som stöds för plats system servrar](../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md).

    > [!NOTE]
    > Installera endast självbetjänings portalen och webbplatsen för administration och övervakning med en primär plats databas. I en-hierarki installerar du de här webbplatserna för varje primär plats.

- Installera [Microsoft ASP.NET MVC 4,0](https://docs.microsoft.com/aspnet/mvc/mvc4)på den webb server som ska vara värd för självbetjänings portalen.

- Det användar konto som kör Portal installations skriptet måste ha SQL **sysadmin** -behörighet på plats databas servern. Under installationen anger skriptet inloggnings-, användar-och SQL-roll rättigheter för webb serverns dator konto. Du kan ta bort det här användar kontot från sysadmin-rollen när du har slutfört installationen av självbetjänings portalen och webbplatsen för administration och övervakning.

- BitLocker-hantering stöds inte på virtuella datorer. Därför kanske vissa funktioner inte fungerar som förväntat på virtuella datorer. BitLocker-hanteringen kommer till exempel inte att starta krypteringen på fasta enheter av virtuella datorer. Ytterligare fasta enheter på virtuella datorer kan visas som kompatibla även om de inte är krypterade.

> [!TIP]
> Som standard krypterar steget **Aktivera BitLocker** endast *använt utrymme* på enheten. BitLocker-hanteringen använder *fullständig disk* kryptering. Konfigurera den här aktivitetssekvensen för att aktivera alternativet att **använda fullständig disk kryptering**. Mer information finns i avsnittet om [aktivitetssekvenser – aktivera BitLocker](../../osd/understand/task-sequence-steps.md#BKMK_EnableBitLocker).

## <a name="next-steps"></a>Nästa steg

[Kryptera återställnings data](../deploy-use/bitlocker/encrypt-recovery-data.md) (ett valfritt krav innan du distribuerar principen för första gången)

[Distribuera klienten för BitLocker-hantering](../deploy-use/bitlocker/deploy-management-agent.md)
