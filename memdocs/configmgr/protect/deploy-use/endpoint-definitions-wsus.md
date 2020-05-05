---
title: Definitioner av Endpoint Protection skadlig kod från WSUS
titleSuffix: Configuration Manager
ms.date: 04/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a34d9401-83e4-471d-8e23-b8042fc11c90
author: mestew
ms.author: mstewart
description: Lär dig hur du konfigurerar Windows Server Update Services för att automatiskt godkänna definitions uppdateringar.
manager: dougeby
ms.openlocfilehash: 235caff52b877177b92792bf8d9fb3a2007127a5
ms.sourcegitcommit: 2871a17e43b2625a5850a41a9aff447c8ca44820
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/24/2020
ms.locfileid: "82126028"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-wsus-for-configuration-manager"></a>Aktivera definitioner av Endpoint Protection skadlig kod för att ladda ned från WSUS för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Om du använder WSUS för att uppdatera definitioner för skadlig kod kan du konfigurera det för att godkänna uppdateringar automatiskt. Även om du använder Configuration Manager program uppdateringar är den rekommenderade metoden för att hålla definitionerna uppdaterade, kan du även konfigurera WSUS som en metod för att tillåta användare att manuellt uppdatera definitioner. Använd följande processer för att konfigurera WSUS som en definitionsuppdateringskälla.

## <a name="synchronize-definition-updates-for-configuration-manager"></a>Synkronisera definitions uppdateringar för Configuration Manager

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj sedan **platser**.

1. Välj den plats som innehåller programuppdateringsplatsen. I gruppen **Inställningar** i menyfliksområdet väljer du **Konfigurera plats komponenter**och väljer sedan **program uppdaterings plats**.

1. I fönstret **Egenskaper för komponent för program uppdaterings plats** växlar du till fliken **klassificeringar** . Välj **definitions uppdateringar**.

1. Om du vill ange de **produkter** som uppdateras med WSUS växlar du till fliken **produkter** .

    - För Windows 10 och senare: Välj **Windows Defender**Under Microsoft > Windows.

    - För Windows 8,1 och tidigare: i Microsoft > Forefront väljer du **System Center Endpoint Protection**.

1. Välj **OK** för att stänga fönstret **Egenskaper för komponenten för program uppdaterings plats** .

## <a name="synchronize-definition-updates-for-standalone-wsus"></a>Synkronisera definitions uppdateringar för fristående WSUS

Använd följande procedur för att konfigurera Endpoint Protection-uppdateringar när WSUS-servern inte är integrerad i din Configuration Manager-miljö.

1. I administrations konsolen för WSUS expanderar du **datorer**, väljer **alternativ**och väljer sedan **produkter och klassificeringar**.

1. Om du vill ange de **produkter** som uppdateras med WSUS växlar du till fliken **produkter** .

    - För Windows 10 och senare: Välj **Windows Defender**Under Microsoft > Windows.

    - För Windows 8,1 och tidigare: i Microsoft > Forefront väljer du **System Center Endpoint Protection**.

1. Växla till fliken **klassificeringar** . Välj **definitions uppdateringar** och **uppdateringar**.

## <a name="approve-definition-updates"></a>Godkänn definitions uppdateringar

Endpoint Protection definitions uppdateringar måste godkännas och hämtas till WSUS-servern innan de erbjuds till klienter som begär listan över tillgängliga uppdateringar. Klienterna ansluter till WSUS-servern för att söka efter uppdateringar och begär sedan de senaste godkända definitionsuppdateringarna.

### <a name="approve-definitions-and-updates-in-wsus"></a>Godkänn definitioner och uppdateringar i WSUS

1. I administrations konsolen för WSUS väljer du **uppdateringar**. Välj sedan **alla uppdateringar** eller den klassificering av uppdateringar som du vill godkänna.

1. I listan över uppdateringar högerklickar du på de uppdateringar eller uppdateringar som du vill godkänna för installation och väljer sedan **Godkänn**.

1. I fönstret **Godkänn uppdateringar** väljer du den dator grupp som du vill godkänna uppdateringarna för och väljer sedan **godkänd för installation**.

### <a name="configure-an-automatic-approval-rule"></a>Konfigurera en regel för automatiskt godkännande

Du kan också ange en regel för automatiskt godkännande för definitions uppdateringar och Endpoint Protection uppdateringar. Den här åtgärden konfigurerar WSUS till att automatiskt godkänna Endpoint Protection definitions uppdateringar som hämtas av WSUS.

1. I administrations konsolen för WSUS väljer du **alternativ**och sedan **automatiska godkännanden**.

1. På fliken **uppdaterings regler** väljer du **ny regel**.

1. I fönstret **Lägg till regel** , under **steg 1: Välj egenskaper**, väljer du alternativet: **när en uppdatering är i en speciell klassificering**.

    1. Under **steg 2: redigera egenskaperna väljer du** **vilken klassificering som helst**.

    1. Avmarkera alla alternativ utom **definitions uppdateringar**och välj sedan **OK**.

1. I fönstret **Lägg till regel** , under **steg 1: Välj egenskaper**, väljer du alternativet: **när en uppdatering finns i en speciell produkt**.

    1. Under **steg 2: redigera egenskaperna väljer du** **valfri produkt**.

    1. Avmarkera alla alternativ utom **System Center Endpoint Protection** för Windows 8,1 och tidigare eller **Windows Defender** för Windows 10 och senare. Välj sedan **OK**.

1. Under **steg 3: Ange ett namn**anger du ett namn för regeln och väljer sedan **OK**.

1. I dialog rutan **automatiska godkännanden** väljer du den nya regeln och väljer sedan **Kör regel**.

> [!NOTE]
> Om du vill maximera prestandan på WSUS-servern och klientdatorerna avvisar du gamla definitionsuppdateringar. Det gör du genom att konfigurera automatiskt godkännande för ändringar och automatisk avvisning av uppdateringar som har slutat gälla. Mer information finns i [Microsoft Support artikel 938947](https://support.microsoft.com/kb/938947).

> [!div class="nextstepaction"]
> [Skapa och distribuera principer för program mot skadlig kod](endpoint-antimalware-policies.md)
