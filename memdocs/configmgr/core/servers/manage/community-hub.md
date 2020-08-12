---
title: Community Hub och GitHub
titleSuffix: Configuration Manager
description: Aktivera och Använd community Hub i Configuration Manager
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 88cead9a-64fe-471e-b57c-81707cefe46c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ae0abdd4a159759037768c8f27d5643bdf612f6e
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128179"
---
# <a name="community-hub-and-github"></a>Community Hub och GitHub
<!--3555935, 3555936-->

IT-administratörs gruppen har utvecklat en enorm mängd kunskap under åren. I stället för att göra om objekt som skript och rapporter från början har vi skapat ett **Configuration Manager community-hubb** där IT-administratörer kan dela med varandra. Genom att använda arbetet med andra kan du spara arbets timmar. Community-hubben utvecklar kreativitet genom att bygga vidare på andra arbete och låta andra personer bygga på din. GitHub har redan branschspecifika processer och verktyg som skapats för delning. Nu kommer community-navet att utnyttja dessa verktyg direkt i Configuration Manager-konsolen som grundläggande delar för att driva den nya gruppen. För den första versionen kommer det innehåll som görs tillgängligt i Community Hub endast att överföras av Microsoft. I framtiden kommer IT-administratörer att kunna överföra innehåll på egen hand med hjälp av ett eget GitHub-konto.

> [!Note]  
> Community Hub är en valfri molnbaserad funktion. Den infördes första gången i juni 2020. Information om hur du väljer community-hubb finns i [valfria funktioner](install-in-console-updates.md#bkmk_options).

## <a name="about-community-hub"></a>Om community Hub

Community Hub stöder följande objekt:

- CMPivot-frågor
- Program
- Aktivitetssekvenser
- Konfigurationsobjekt
- PowerShell-skript
- Rapporter

## <a name="prerequisites"></a>Förutsättningar

- Enheten som kör Configuration Manager-konsolen som används för att få åtkomst till community Hub behöver följande objekt:
   - .NET Framework version 4,6 eller senare
   - Windows 10 version 17110 eller senare
      - Windows Server stöds inte, så Configuration Manager-konsolen måste installeras på en Windows 10-enhet separat från plats servern.
   - Det inloggade användar kontot får inte vara det inbyggda administratörs kontot

- [Administrations tjänsten](../../../develop/adminservice/set-up.md) i Configuration Manager måste konfigureras och fungera.

- Om din organisation begränsar nätverkskommunikation med Internet med en brand vägg eller proxyserver, måste du tillåta att Configuration Manager-konsolen får åtkomst till Internet-slutpunkter. Mer information finns i [krav för Internet åtkomst](../../plan-design/network/internet-endpoints.md#community-hub).

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


## <a name="direct-links-to-community-hub-items"></a><a name="bkmk_deeplink"></a>Direkta länkar till community Hub-objekt
<!--4224406-->
*(Lanseras i version 2006)* Du kan enkelt navigera till och referens objekt i noden Configuration Manager-konsolen community Hub med en direkt länk. Avsikten med den här funktionen är för enklare samarbete och kan dela länkar till community Hub-objekt med dina kollegor. De här djup länkarna är för närvarande bara för objekt i Community Hub-noden i-konsolen.

### <a name="prerequisites-for-direct-links"></a>Krav för direkt länkar

- Configuration Manager-konsol version 2006 eller senare
- Du kan inte använda det lokala inbyggda administratörs kontot när du följer en community Hub-länk.

### <a name="sharing-and-opening-direct-links"></a>Dela och öppna direkt länkar

Så här delar du ett objekt:
1. Gå till objektet i hubben och välj **dela**.
1. Klistra in den kopierade länken och dela den med andra.

Så här öppnar du en delad länk:
1. Klicka på länken från en dator där Configuration Manager-konsolen är installerad.
   - Använd till exempel den här länken för att dela [konfigurations skriptet för den automatiska uppdateringen](https://communityhub.microsoft.com/item/7200) ( `https://communityhub.microsoft.com/item/7200` ).
1. Välj **Starta community Hub** när du uppmanas till det.
1. Konsolen öppnas direkt till skriptet i Community-hubben.

## <a name="known-issues"></a><a name="bkmk_known"></a>Kända problem

### <a name="unable-to-access-community-hub-node-when-running-console-as-a-different-user"></a>Det går inte att komma åt community Hub-noden när konsolen körs som en annan användare
<!--7826897-->
Om du är inloggad som en användare med lägre rättigheter och väljer **Kör som** en annan användare för att öppna Configuration Manager-konsolen kanske du inte kan komma åt **Community Hub** -noden.

### <a name="downloaded-reports-dont-get-removed-from-your-downloads-page"></a>Hämtade rapporter tas inte bort från nedladdnings Sidan
<!--7851305-->
Om du tar bort en nedladdad rapport från noden **övervaknings**  >  **rapporter** tas rapporten inte bort från **Community-hubben**  >  **nedladdnings** sidan och du kan inte ladda ned rapporten igen. 

## <a name="next-steps"></a>Nästa steg

Lär dig mer om att skapa och använda följande objekt:

- [Skapa och kör PowerShell-skript](../../../apps/deploy-use/create-deploy-scripts.md)
- [Introduktion till rapportering](introduction-to-reporting.md)
- [Skapa och hantera aktivitetssekvenser](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md)
- [Skapa och distribuera ett program](../../../apps/get-started/create-and-deploy-an-application.md)
- [Skapa konfigurationsobjekt](../../../compliance/deploy-use/create-configuration-items.md)