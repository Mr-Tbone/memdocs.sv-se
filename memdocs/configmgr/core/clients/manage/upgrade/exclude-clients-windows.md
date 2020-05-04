---
title: Undanta klient uppgraderingar för Windows
titleSuffix: Configuration Manager
description: Lär dig hur du undantar Windows-klienter från att uppgraderas i Configuration Manager.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4cd6031f-8844-4d0b-8166-b24d6528a94e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 58a7741bb628a0c8fb346c8f61b446301b138d80
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715419"
---
# <a name="how-to-exclude-clients-from-upgrade-in-configuration-manager"></a>Så här undantar du klienter från uppgradering i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Du kan undanta en samling klienter från att automatiskt installera uppdaterade klient versioner. Använd detta undantag för en samling datorer som behöver bättre försiktighet vid uppgradering av-klienten. En klient som ingår i en undantagen samling ignorerar förfrågningar om att installera uppdaterad klient program vara.

Detta undantag gäller följande metoder:

- Automatisk uppgradering
- Uppgradering baserad på program uppdatering
- Inloggnings skript
- Grup princip

> [!NOTE]
> Även om användar gränssnittet säger att klienterna inte uppgraderas via någon metod, finns det två metoder som du kan använda för att åsidosätta inställningarna. Använd klient-push eller manuell klient installation för att åsidosätta den här konfigurationen. Mer information finns i [så här uppgraderar du en undantagen klient](#bkmk_override).

## <a name="configure-exclusion"></a><a name="bkmk_exclude"></a>Konfigurera undantag

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen. Expandera **plats konfiguration**, välj noden **platser** och välj sedan inställningar för **hierarki** i menyfliksområdet.

2. Växla till fliken **klient uppgradering** .

3. Välj alternativet för att **undanta angivna klienter från uppgradering**. Välj sedan den **undantags samling** som du vill undanta. Du kan bara välja en samling som ska undantas.

4. Välj **OK** för att stänga och spara konfigurationen.

![Inställningar för undantag för automatisk uppgradering](media/automatic_upgrade_exclusion.png)

När klienterna i den undantagna samlingens uppdaterings princip inte installerar klient uppdateringar automatiskt. Mer information finns i [Uppgradera klienter för Windows-datorer](upgrade-clients-for-windows-computers.md).

> [!NOTE]
> Exkluderade klienter kan fortfarande ladda ned och köra CCMSetup, men inte uppgradera.

När du tar bort en klient från exkluderings samlingen uppgraderas den inte automatiskt till nästa automatiska uppgraderings cykel.

## <a name="how-to-upgrade-an-excluded-client"></a><a name="bkmk_override"></a>Så här uppgraderar du en undantagen klient

Om en enhet är medlem i en samling som du har exkluderat från uppgraderingen kan du fortfarande uppgradera klienten med någon av följande metoder:

- **Push-installation av klient**: CCMSetup tillåter push-installation av klienter eftersom det är din direkta avsikt. Med den här metoden kan du uppgradera en klient utan att ta bort den från samlingen eller ta bort hela samlingen från undantag.

- **Manuell klient installation**: uppgradera en undantagen klient manuellt med hjälp av följande kommando rads parameter för CCMSetup: **/IgnoreSkipUpgrade**

    Om du försöker uppgradera en klient som är medlem i den exkluderade samlingen manuellt och inte använder den här parametern, uppgraderas inte klienten. Mer information finns i [så här installerar du Configuration Manager klienter manuellt](../../deploy/deploy-clients-to-windows-computers.md#BKMK_Manual).

## <a name="see-also"></a>Se även

- [Uppgradera klienter](upgrade-clients.md)

- [Distribuera klienter på Windows-datorer](../../deploy/deploy-clients-to-windows-computers.md)

- [Utökad samverkansklient](../../../understand/interoperability-client.md)
