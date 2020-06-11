---
title: Community Hub och GitHub
titleSuffix: Configuration Manager
description: Aktivera och Använd community Hub i Configuration Manager
ms.date: 06/10/2020
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 88cead9a-64fe-471e-b57c-81707cefe46c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 606c9490e56d932176b17eef95ea4ed0c956770e
ms.sourcegitcommit: a198e4efa52b16f87049853b9d8c9854fd9fa057
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/11/2020
ms.locfileid: "84680429"
---
# <a name="community-hub-and-github"></a>Community Hub och GitHub
<!--3555935, 3555936-->

IT-administratörs gruppen har utvecklat en enorm mängd kunskap under åren. I stället för att göra om objekt som skript och rapporter från början har vi skapat ett **Configuration Manager community-hubb** där IT-administratörer kan dela med varandra. Genom att använda arbetet med andra kan du spara arbets timmar. Community-hubben utvecklar kreativitet genom att bygga vidare på andra arbete och låta andra personer bygga på din. GitHub har redan branschspecifika processer och verktyg som skapats för delning. Nu kommer community-navet att utnyttja dessa verktyg direkt i Configuration Manager-konsolen som grundläggande delar för att driva den nya gruppen. För den första versionen kommer det innehåll som görs tillgängligt i Community Hub endast att överföras av Microsoft. I framtiden kommer IT-administratörer att kunna överföra innehåll på egen hand med hjälp av ett eget GitHub-konto.

> [!Note]  
> Community Hub är en valfri molnbaserad funktion. Den infördes första gången i juni 2020. Information om hur du väljer community-hubb finns i [valfria funktioner](install-in-console-updates.md#bkmk_options).

## <a name="about-community-hub"></a>Om community Hub

Community Hub stöder följande objekt:
- PowerShell-skript
- Rapporter
- Aktivitetssekvenser
- Program
- Konfigurationsobjekt  

## <a name="prerequisites"></a>Krav

- Enheten som kör Configuration Manager-konsolen som används för att få åtkomst till community Hub behöver följande objekt:
   - .NET Framework version 4,6 eller senare
   - Windows 10 version 17110 eller senare
      - Windows Server stöds inte, så Configuration Manager-konsolen måste installeras på en Windows 10-enhet separat från plats servern.
   - Det inloggade användar kontot får inte vara det inbyggda administratörs kontot

- Om du vill hämta rapporter måste du aktivera alternativet **använd Configuration Manager-genererade certifikat för HTTP-platssystem** på den plats som du importerar till. Mer information finns i [Enhanced http](/sccm/core/plan-design/hierarchy/enhanced-http).
   1. Gå till **Administration**  >  **plats konfiguration**  >  **platser**.
   1. Välj platsen och välj **Egenskaper** i menyfliksområdet.
   1. På fliken **kommunikations säkerhet** väljer du alternativet för att **använda Configuration Manager-genererade certifikat för http-platssystem**.

## <a name="permissions"></a>Behörigheter

- Så här importerar du ett skript: **skapa** behörighet för **SMS_Scripts** -klass.
- Importera en rapport: säkerhets rollen fullständig administratör.


## <a name="use-the-community-hub"></a>Använd community-hubben

1. Gå till **Community Hub** -noden i **Community** -arbetsytan.
1. Välj ett objekt att ladda ned.
1. Du behöver rätt behörigheter på Configuration Managers platsen för att kunna ladda ned objekt från hubben och importera dem till webbplatsen.
    - Så här importerar du ett skript: **skapa** behörighet för SMS_Scripts-klass.
    - Importera en rapport: säkerhets rollen fullständig administratör.
1. Nedladdade rapporter distribueras till en rapportmapp som kallas **hubb** på repor ting Services-platsen. Hämtade skript kan visas i noden **Kör skript** .
1. Visa alla objekt som hämtats från hubben av din organisation genom att klicka på **dina nedladdningar** från **Community Hub** -noden.

[![Alla objekt som hämtats från community-hubben](./media/3555935-community-hub-downloads.png)](./media/3555935-community-hub-downloads.png#lightbox)


## <a name="next-steps"></a>Nästa steg

Lär dig mer om att skapa och använda följande objekt:

- [Skapa och kör PowerShell-skript](../../../apps/deploy-use/create-deploy-scripts.md)
- [Introduktion till rapportering](introduction-to-reporting.md)
- [Skapa och hantera aktivitetssekvenser](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md)
- [Skapa och distribuera ett program](../../../apps/get-started/create-and-deploy-an-application.md)
- [Skapa konfigurationsobjekt](../../../compliance/deploy-use/create-configuration-items.md)