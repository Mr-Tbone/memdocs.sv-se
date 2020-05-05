---
title: Själv service portal för BitLocker
titleSuffix: Configuration Manager
description: Använda självbetjänings portalen för användare i Configuration Manager för BitLocker-återställning
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 88e0ad46-7f0c-4f5c-9b48-54773c23768d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fda719aed4d70cd9783d158e17d546b698497997
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717407"
---
# <a name="bitlocker-self-service-portal"></a>Själv service portal för BitLocker

*Gäller för: Configuration Manager (aktuell gren)*

<!--3601034-->

När du har [installerat självbetjänings portalen för BitLocker](setup-websites.md), om BitLocker låser en användares enhet, kan de oberoende få åtkomst till sina datorer. Självbetjänings portalen kräver ingen hjälp från support personalen.

[![Skärm bild av standard tjänst portalen för BitLocker](media/bitlocker-self-service-portal.png)](media/bitlocker-self-service-portal.png#lightbox)

> [!IMPORTANT]
> För att få en återställnings nyckel från självbetjänings portalen måste en användare ha loggat in på datorn minst en gång. Den här inloggningen måste vara lokal på enheten, inte i en fjärrsession. Annars behöver de Kontakta supportavdelningen för nyckel återställning. En support administratör kan använda webbplatsen för [administration och övervakning](helpdesk-portal.md) för att begära återställnings nyckeln.

BitLocker kan låsa enheten i följande situationer:

- Användaren glömmer bort lösen ordet eller PIN-koden för BitLocker

- Det finns en ändring av enhetens OS-filer, BIOS eller Trusted Platform Module (TPM)

Så här begär du BitLocker-återställnings nyckeln från självbetjänings portalen:

1. När BitLocker låser en enhet visas BitLocker-återställnings skärmen under start. Skriv ner den 32-siffriga återställnings nyckeln för BitLocker-återställning.

1. På en annan dator går du till självbetjänings portalen i webbläsaren, till exempel `https://webserver.contoso.com/SelfService`.

1. Läs och godkänn meddelandet.

1. I fältet **återställnings nyckel-ID** anger du de första åtta siffrorna i ID: t för BitLocker-återställnings nyckeln. Om den matchar flera nycklar anger du alla 32 siffror.

1. Välj ett av följande alternativ för **orsaken** till den här begäran:

    - BIOS/TPM har ändrats
    - Operativ systemet har ändrats
    - Förlorad PIN/lösen fras

1. Välj **Hämta nyckel**. Självbetjänings portalen visar den 48-siffriga **återställnings nyckeln för BitLocker**.

1. Ange den här 48-siffriga koden i BitLocker-återställnings skärmen på din dator.

> [!NOTE]
> Installations-och självbetjänings portalen för BitLocker kan stängas av efter en tids inaktivitet. Om du till exempel har fem minuter kan du se en tids gräns varning med en räknare på 60 sekunder.
>
> ![Varning om tids gräns för BitLocker-självbetjänings Portal](media/bitlocker-self-service-portal-timeout-warning.png)
>
> Om du inte svarar på nedräkningen upphör sessionen att gälla.
>
> ![Installations sidan för självbetjänings portalen för BitLocker har förfallit](media/bitlocker-self-service-portal-session-expired.png)
