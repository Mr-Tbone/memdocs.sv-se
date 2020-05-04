---
title: Hantera synkronisering av program uppdateringar
titleSuffix: Configuration Manager
description: Använd de här stegen för att schemalägga synkronisering av program uppdateringar, starta synkroniseringen av program uppdateringar manuellt och övervaka synkroniseringen av program uppdateringar.
ms.date: 12/20/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: ea8698c4-9df5-4cf5-8b62-ab93115b4769
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: d1b47965fa5cc36b0c0eb6d47c2214d1dceb8ee8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712682"
---
#  <a name="synchronize-software-updates"></a><a name="BKMK_SUMSync"></a>Synkronisera program uppdateringar

*Gäller för: Configuration Manager (aktuell gren)*

 Synkronisering av program uppdatering i Configuration Manager är en process för att hämta metadata för program uppdateringen som uppfyller de kriterier som du konfigurerar. Detta inkluderar vissa produkter, klassificeringar och språk. Normalt hämtar program uppdaterings platsen på den centrala administrations platsen eller på en fristående primär plats metadata från Microsoft Update. Sedan kommer platsen på den översta nivån att skicka en synkroniseringsbegäran till andra platser. När en plats tar emot synkroniseringsbegäran från den överordnade platsen hämtar program uppdaterings platsen för platsen program uppdateringens metadata från den överordnade [synkroniseringens synkroniserings källa](../plan-design/plan-for-software-updates.md#BKMK_SyncSource). Mer information om processen för synkronisering av program uppdateringar finns i [synkronisering av program uppdateringar](../understand/software-updates-introduction.md#BKMK_Synchronization).

Du konfigurerar synkronisering av program uppdatering så att den körs enligt ett schema i egenskaperna för program uppdaterings platsen på platsen på den översta nivån. När du har konfigurerat synkroniseringsschemat ändrar du normalt inte schemat som en del av de normala åtgärderna. Du kan dock starta synkroniseringen av program uppdateringar manuellt när det behövs.

  > [!NOTE]  
  >  Program uppdaterings platser måste vara anslutna till den överordnade synkroniseringstjänsten för att synkronisera program uppdateringar. När en programuppdateringsplats är bortkopplad från dess överordnade synkroniseringskälla kan du synkronisera programuppdateringar med import- och exportmetoden. Mer information finns i avsnittet [Synkronisera programuppdateringar från en frånkopplad programuppdateringsplats](synchronize-software-updates-disconnected.md).  

## <a name="schedule-software-updates-synchronization"></a>Schemalägga synkronisering av program uppdateringar
När du konfigurerar ett schema för synkronisering av program uppdateringar, startar program uppdaterings platsen på den översta nivån synkroniseringen med Microsoft Update vid det schemalagda datumet och tidpunkten. Med det anpassade schemat kan du synkronisera program uppdateringar på ett datum och en tid när kraven för Windows Server Update Services (WSUS)-servern, plats servern och nätverket är låga. Du kan till exempel ställa in schemat så att program uppdateringarna synkroniseras varje vecka kl. 2:00. Under den schemalagda synkroniseringen förs alla ändringar av metadata för programuppdateringarna sedan den senaste schemalagda synkroniseringen in i platsdatabasen. Detta inbegriper nya programuppdateringsmetadata eller metadata som har ändrats, tagits bort eller upphört att gälla.

Använd följande procedurer på platsen på den högsta nivån för att schemalägga synkronisering av program uppdateringar.  

#### <a name="to-schedule-software-updates-synchronization"></a>Schemalägga synkronisering av programuppdateringar  

  1.  Klicka på **Administration**i Configuration Manager-konsolen.  

  2.  I arbetsytan Administration expanderar du **Platskonfiguration**och klickar sedan på **Platser**.  

  3.  Klicka på den centrala administrationsplatsen eller på den fristående primära platsen i resultatfönstret.  

  4.  På fliken **Start** i gruppen **Inställningar** expanderar du **Konfigurera platskomponenter**och klickar sedan på **Programuppdateringsplats**.  

  5.  Välj **Aktivera synkronisering enligt schema**i dialogrutan Egenskaper för platskomponent för programuppdatering och ange sedan synkroniseringsschemat.  

## <a name="manually-start-software-updates-synchronization"></a>Starta synkroniseringen av program uppdateringar manuellt
Du kan initiera synkroniseringen av program uppdateringar manuellt på platsen på den översta nivån i Configuration Manager-konsolen från noden **alla program uppdateringar** i arbets ytan **program varu bibliotek** .  

Använd följande procedurer på platsen på den översta nivån för att initiera synkroniseringen av program uppdateringar manuellt.  

#### <a name="to-manually-start-software-updates-synchronization"></a>Starta synkroniseringen av program uppdateringar manuellt  

1. I Configuration Manager-konsolen som är ansluten till den centrala administrations platsen eller den fristående primära platsen klickar du på **program varu bibliotek**.  

2. Expandera **Programuppdateringar** på arbetsytan Programvarubibliotek och klicka på **Alla programuppdateringar** eller **Programuppdateringsgrupper**.  

3. Gå till gruppen **Skapa** på fliken **Start** och klicka på **Synkronisera programuppdateringar**. Bekräfta att du vill initiera synkroniseringsprocessen genom att klicka på **Ja** i dialogrutan.  

   När du har initierat synkroniseringsprocessen på program uppdaterings platsen kan du övervaka synkroniseringsprocessen från Configuration Manager-konsolen för alla program uppdaterings platser i hierarkin. Använd följande procedur om du vill övervaka processen för synkronisering av programuppdateringar.  


## <a name="monitor-software-updates-synchronization"></a>Övervaka synkronisering av program uppdateringar
När du har initierat synkroniseringsprocessen kan du använda Configuration Manager-konsolen för att övervaka processen för alla program uppdaterings platser i hierarkin. Använd följande procedur för att övervaka synkroniseringsprocessen för programuppdatering. Mer information om övervakning av program uppdateringar, inklusive synkroniseringsprocessen, finns i [övervaka program uppdateringar](../deploy-use/monitor-software-updates.md).

#### <a name="to-monitor-the-software-updates-synchronization-process"></a>Övervaka processen för synkronisering av programuppdateringar  

1. Klicka på **övervakning**i Configuration Manager-konsolen.  

2. Klicka på **synkroniseringsstatus för program uppdaterings punkt**på arbets ytan **övervakning** .  

   Program uppdaterings platserna i Configuration Manager hierarkin visas i resultat fönstret. Från den här vyn kan du övervaka synkroniseringsstatusen för alla programuppdateringsplatser. Om du vill har mer detaljerad information om synkroniseringsprocessen kan du granska den wsyncmgr.log-fil som finns i <*ConfigMgrInstallationPath*>\Logs på varje platsserver.  

## <a name="import-updates-from-the-microsoft-update-catalog"></a>Importera uppdateringar från Microsoft Updates katalogen

Program uppdaterings platsen på den översta nivån använder WSUS för att hämta information om program uppdateringar från Microsoft till Configuration Manager. Ibland kan du behöva en uppdatering som inte automatiskt synkroniseras med WSUS för de valda produkterna och klassificeringarna, men är tillgänglig i [Microsoft Update katalogen](https://catalog.update.microsoft.com). Uppdateringar som inte synkroniseras automatiskt till WSUS är vanligt vis avsedda att lösa mycket specifika problem. Om det finns en uppdatering i katalogen kan du importera den till WSUS. Du kan sedan synkronisera den till Configuration Manager och distribuera den som vilken annan uppdatering som helst.

### <a name="to-import-an-update-from-the-microsoft-update-catalog"></a>Så här importerar du en uppdatering från Microsoft Updates katalogen

1. Öppna WSUS-administratörskonsolen och Anslut den till WSUS-servern på den översta nivån i hierarkin.
   - Om Internet Explorer inte är datorns standard webbläsare anger du tillfälligt den som standard.
2. Klicka på **uppdateringar** eller klicka på namnet på din WSUS-server. 
3. I fönstret **åtgärder** väljer du **Importera uppdateringar...** som öppnar ett webbläsarfönster till [Microsoft Update katalogen](https://catalog.update.microsoft.com).
   ![Välj Importera uppdateringar i WSUS-konsolen](media/wsus-console-import-updates.png)
4. Om du uppmanas att installera Microsoft Update Catalog ActiveX-kontrollen. Kontrollen måste vara installerad för att importera uppdateringar till WSUS. 
5. I webbläsarfönstret söker du efter den uppdatering som du vill använda. Klicka på knappen **Lägg till*** för att lägga till den i korgen.
6. Klicka på **Visa korg**. Se till att alternativet att **Importera direkt till Windows Server Update Services** är markerat. Klicka sedan på **Importera**.
    ![Importera uppdatering från katalogen till WSUS](./media/import-catalog-update-into-wsus.png)
7. När importen är klar klickar du på **Stäng** i webbläsarfönstret.
     - Återställ din standard webbläsare om det behövs.
8. Synkronisera din Configuration Manager program uppdaterings plats.


## <a name="next-steps"></a>Nästa steg
När du har synkroniserat program uppdateringar för första gången, eller när det finns nya klassificeringar eller produkter tillgängliga, måste du [Konfigurera de nya klassificeringarna och produkterna](configure-classifications-and-products.md) för att synkronisera program uppdateringar med de nya kriterierna.

När du har synkroniserat program uppdateringar med de villkor som du behöver [hanterar du inställningar för program uppdateringar](manage-settings-for-software-updates.md).  
