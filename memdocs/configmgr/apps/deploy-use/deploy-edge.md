---
title: Distribuera och uppdatera Microsoft Edge, version 77 och senare
titleSuffix: Configuration Manager
description: Distribuera och uppdatera Microsoft Edge, version 77 och senare med Configuration Manager
ms.date: 07/02/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 73b420be-5d6a-483a-be66-c4d274437508
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: cc10f262e4639ffdd8513bece662116f5ed39516
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695383"
---
# <a name="microsoft-edge-management"></a>Microsoft Edge-hantering

*Gäller för: Configuration Manager (Current Branch)*

Det nya Microsoft Edge är klart för företag. Från och med Configuration Manager version 1910 kan du nu distribuera [Microsoft Edge, version 77 och senare](/deployedge/) till dina användare. Ett PowerShell-skript används för att installera Edge-versionen som valts. Skriptet stänger också av automatiska uppdateringar för kant så att de kan hanteras med Configuration Manager.

## <a name="deploy-microsoft-edge"></a><a name="bkmk_Microsoft_Edge"></a> Distribuera Microsoft Edge
<!--4561024-->
Administratörer kan välja beta-, dev-eller stabil kanal, tillsammans med en version av Microsoft Edge-klienten som ska distribueras. I varje utgåva ingår information och förbättringar från våra kunder och community.

### <a name="prerequisites-for-deploying"></a>Krav för distribution

För klienter riktade till en Microsoft Edge-distribution:

- Det går inte att ange en begränsning för [körnings principen](/powershell/module/microsoft.powershell.core/about/about_execution_policies) för PowerShell.
  - PowerShell körs för att utföra installationen.

- Installations-och [CMPivot](../../core/servers/manage/cmpivot.md) för Microsoft Edge är signerade med **Microsofts kod signerings** certifikat. Om certifikatet inte visas i arkivet **Betrodda utgivare** måste du lägga till det. Annars körs inte installations programmet för Microsoft Edge och CMPivot när PowerShell-körnings principen är inställd på **AllSigned**. <!--7585106-->

Enheten som kör Configuration Managers konsolen behöver åtkomst till följande slut punkter:

|Plats|Användning|
|---|---|
|`https://edgeupdates.microsoft.com/api/products?view=enterprise`|Information om utgåvor av Microsoft Edge|
|`http://dl.delivery.mp.microsoft.com`|Innehåll för Microsoft Edge-versioner|

### <a name="verify-microsoft-edge-update-policies"></a><a name="bkmk_autoupdate"></a> Verifiera uppdaterings principer för Microsoft Edge

#### <a name="configuration-manager-version-1910"></a>Configuration Manager version 1910

När Microsoft Edge distribueras i version 1910 stänger installations skriptet av automatiska uppdateringar för Microsoft Edge så att de kan hanteras med Configuration Manager. Du kan ändra det här beteendet med hjälp av grupprincip. Mer information finns i [Planera distributionen av Microsoft Edge](/deployedge/deploy-edge-plan-deployment#define-and-configure-policies) -och [Microsoft Edge-uppdaterings principer](/DeployEdge/microsoft-edge-update-policies).

#### <a name="configuration-manager-version-2002-and-later"></a>Configuration Manager version 2002 och senare
<!--4561024-->
Från och med version 2002 kan du skapa ett Microsoft Edge-program som har kon figurer ATS för att ta emot automatiska uppdateringar i stället för att automatiska uppdateringar har inaktiverats. Med den här ändringen kan du välja att hantera uppdateringar för Microsoft Edge med Configuration Manager eller tillåta att Microsoft Edge uppdateras automatiskt. När du skapar programmet väljer **du Tillåt att Microsoft Edge automatiskt uppdaterar versionen av klienten på slutanvändarens enhet** på sidan med inställningar för **Microsoft Edge** . Om du tidigare använde grupprincip för att ändra det här beteendet, skriver grupprincip över inställningen som gjorts av Configuration Manager under installationen av Microsoft Edge.

[![Inställning för automatisk uppdatering av Microsoft Edge](./media/4561024-autoupdate-edge.png)](./media/4561024-autoupdate-edge.png#lightbox)

### <a name="create-a-deployment"></a>Skapa en distribution

Skapa ett Microsoft Edge-program med hjälp av den inbyggda program upplevelsen som gör Microsoft Edge lättare att hantera:

1. I-konsolen, under **program bibliotek**, finns en ny nod som heter **Microsoft Edge Management**.
1. Välj **skapa Microsoft Edge-program** från menyfliken eller genom att högerklicka på **Microsoft Edge Management** -noden.

   ![Microsoft Edge Management-noden högerklickar på åtgärd](./media/4561024-create-microsoft-edge-application.png)

1. På sidan **program inställningar** i guiden anger du ett namn, en beskrivning och en plats för innehållet för appen. Se till att mappen för innehålls platsen som du anger är tom.
1. På sidan **Inställningar för Microsoft Edge** väljer du:
   - Kanalen som ska distribueras
   - Den version som ska distribueras
   - Om du vill att **Microsoft Edge automatiskt ska uppdatera versionen av klienten på slutanvändarens enhet** (lades till i version 2002)
1. På sidan **distribution** bestämmer du om du vill distribuera programmet. Om du väljer **Ja**kan du ange distributions inställningarna för programmet. Mer information om distributions inställningar finns i [distribuera program](deploy-applications.md#bkmk_deploy-general).
1. I **Software Center** på klient enheten kan användaren se och installera programmet.

   ![Sidan Inställningar för Microsoft Edge i distributions guiden](./media/4561024-software-center-install-edge.png)

### <a name="log-files-for-deployment"></a>Loggfiler för distribution

|Plats|Loggas|Användning|
|---|---|---|
| Platsserver|SMSProv.log|Visar information om skapandet av appen eller distributionen Miss lyckas.|
| [Det varierar](../../core/plan-design/hierarchy/log-files.md)|PatchDownloader.log| Visar information om innehålls hämtningen Miss lyckas|
| Client|  AppEnforce.log|Visar installations information|

## <a name="update-microsoft-edge"></a>Uppdatera Microsoft Edge
<!--4831871-->

Från och med Configuration Manager version 1910 ser du en nod som kallas **alla Microsoft Edge-uppdateringar** under **Microsoft Edge Management**. Den här noden hjälper dig att hantera uppdateringar för alla Microsoft Edge-kanaler.<!--initial edge updates released Jan 15,2020-->

1. Se till att du har **uppdaterings** klassificering och **Microsoft Edge** -produkten [vald för synkronisering](../../sum/get-started/configure-classifications-and-products.md)för att hämta uppdateringar för Microsoft Edge.

   [![Välj Microsoft Edge som produkt i egenskaper för program uppdaterings plats](./media/4831871-microsoft-edge-product-sup.png)](./media/4831871-microsoft-edge-product-sup.png#lightbox)

1. I arbets ytan **program bibliotek** expanderar du **Microsoft Edge Management** och klickar på **alla Microsoft Edge updates** -noden.

1. Om det behövs klickar du på **Synkronisera program uppdateringar** i menyfliksområdet för att starta en synkronisering. Mer information finns i [Synkronisera program uppdateringar](../../sum/get-started/synchronize-software-updates.md).

   ![Alla Microsoft Edge updates-noden](./media/4831871-all-microsoft-edge-updates.png)

1. Hantera och distribuera Microsoft Edge-uppdateringar som andra uppdateringar, till exempel lägga till dem i den [automatiska distributions regeln](../../sum/deploy-use/automatically-deploy-software-updates.md). Några av de vanliga uppdaterings uppgifterna som du kan utföra från **Microsoft Edge updates** -noden är:

   - [Skapa en fasindelad distribution](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)
   - [Distribuera programuppdateringar manuellt](../../sum/deploy-use/manually-deploy-software-updates.md)
   - [Hämta programuppdateringar](../../sum/deploy-use/download-software-updates.md)

## <a name="microsoft-edge-management-dashboard"></a><a name="bkmk_edge-dash"></a> Instrument panel för Microsoft Edge-hantering
<!--3871913-->
*(Lanseras i version 2002)*

Från och med Configuration Manager 2002 ger Microsoft Edge Management-instrumentpanelen dig insikter om användningen av Microsoft Edge och andra webbläsare. I den här instrument panelen kan du:

- Se hur många av dina enheter som har Microsoft Edge installerat
- Se hur många klienter som har olika versioner av Microsoft Edge installerade.
   - Det här diagrammet omfattar inte Kanarie Channel.
- Visa de installerade webbläsarna på olika enheter
- Visa önskad webbläsare efter enhet <!--5907383-->
   - Detta diagram är för närvarande tomt för 2002-versionen.

### <a name="prerequisites-for-the-dashboard"></a>Krav för instrument panelen

Aktivera följande egenskaper i [maskin varu inventerings](../../core/clients/manage/inventory/extend-hardware-inventory.md) klasser för Microsoft Edge Management-instrument panelen:

- **Installerad program vara – Tillgångsinformation (SMS_InstalledSoftware)**
   - Program varu kod
   - Produktnamn
   - Produkt version

- **Standard webbläsare (SMS_DefaultBrowser)**
   - Webb läsar program-ID

- **Webb läsar användning (SMS_BrowserUsage)**
   - BrowserName
   - UsagePercentage

### <a name="view-the-dashboard"></a>Visa instrumentpanelen

I arbets ytan **program bibliotek** klickar du på **Microsoft Edge Management** för att se instrument panelen. Ändra samlingen för diagrammets data genom att klicka på **Bläddra** och välja en annan samling. Som standard är de fem största samlingarna i list rutan. När du väljer en samling som inte finns i listan, visas den nyligen valda samlingen längst ned i list rutan.

[![Instrument panel för Microsoft Edge-hantering](./media/3871913-microsoft-edge-dashboard.png)](./media/3871913-microsoft-edge-dashboard.png#lightbox)

## <a name="known-issues"></a>Kända problem

### <a name="hardware-inventory-may-fail-to-process"></a>Maskin varu inventeringen kanske inte kan bearbeta
<!--7535675-->
Maskin varu inventering för enheter kan inte bearbetas. Fel som liknar dem nedan visas i filen Dataldr. log:

```text
Begin transaction: Machine=<machine>
*** [23000][2627][Microsoft][SQL Server Native Client 11.0][SQL Server]Violation of PRIMARY KEY constraint 'BROWSER_USAGE_HIST_PK'. Cannot insert duplicate key in object 'dbo.BROWSER_USAGE_HIST'. The duplicate key value is (XXXX, Y). : dbo.dBROWSER_USAGE_DATA
ERROR - SQL Error in
ERROR - is NOT retyrable.
Rollback transaction: XXXX
```

**Minskning:** Undvik det här problemet genom att inaktivera insamlingen av maskin varu inventerings klassen för webb läsar användning (SMS_BrowerUsage).

## <a name="next-steps"></a>Nästa steg

[Övervakning av program](monitor-applications-from-the-console.md)

[Övervaka programuppdateringar](../../sum/deploy-use/monitor-software-updates.md)

[Hantera och övervaka fasindelade distributioner](../../osd/deploy-use/manage-monitor-phased-deployments.md)