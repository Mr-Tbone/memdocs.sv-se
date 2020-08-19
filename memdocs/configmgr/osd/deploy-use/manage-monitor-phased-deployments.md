---
title: Hantera stegvisa distributioner av & övervakare
titleSuffix: Configuration Manager
description: Lär dig hur du hanterar och övervakar stegvisa distributioner för program vara i Configuration Manager.
ms.date: 04/16/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: dc245916-bc11-4983-9c4d-015f655007c1
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: fe8bbbf311baa335640ca7dea90ccd46da4fa5ea
ms.sourcegitcommit: 8fc7f2864c5e3f177e6657b684c5f208d6c2a1b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/19/2020
ms.locfileid: "88591718"
---
# <a name="manage-and-monitor-phased-deployments"></a>Hantera och övervaka fasindelade distributioner

Den här artikeln beskriver hur du hanterar och övervakar stegvisa distributioner. Hanterings uppgifter omfattar manuellt inledningen av nästa fas, och pausar eller återupptar en fas. 

Först måste du skapa en stegvis distribution: 
- [Program](create-phased-deployment-for-task-sequence.md?toc=/mem/configmgr/apps/toc.json&bc=/mem/configmgr/apps/breadcrumb/toc.json)  
- [Program uppdatering](create-phased-deployment-for-task-sequence.md?toc=/mem/configmgr/sum/toc.json&bc=/mem/configmgr/sum/breadcrumb/toc.json)  
- [Aktivitetssekvens](create-phased-deployment-for-task-sequence.md)  



## <a name="move-to-the-next-phase"></a><a name="bkmk_move"></a> Gå vidare till nästa fas

När du väljer inställningen **börjar den andra fasen av distributionen manuellt**, platsen startar inte automatiskt nästa fas baserat på lyckade kriterier. Du måste flytta fasen stegvis distribution till nästa fas.  

1. Hur du startar den här åtgärden varierar beroende på typ av distribuerad program vara:  

    - **Program** (endast i version 1806 eller senare): gå till arbets ytan **program varu bibliotek** , expandera **program hantering**och välj **program**.   

    - **Program uppdatering** (endast i version 1810 eller senare): gå till arbets ytan **program varu bibliotek** och välj en av följande noder:    
        - Programuppdateringar  
            - **Alla program uppdateringar**  
            - **Program uppdaterings grupper**   
        - Windows 10-underhåll, **alla Windows 10-uppdateringar**  
        - Office 365-klient hantering, **office 365-uppdateringar**  

    - **Aktivitetssekvens**: gå till arbets ytan **program varu bibliotek** , expandera **operativ system**och välj **aktivitetssekvenser**.   

2. Välj program varan med den stegvisa distributionen.  

3. I informations fönstret växlar du till fliken stegvisa **distributioner** .  

4. Välj fasen stegvis distribution och klicka på **Flytta till nästa fas** i menyfliksområdet.  

    ![Högerklicka på meny som visar åtgärder för en stegvis distribution](media/Suspend-phased-deployment.PNG)



## <a name="suspend-and-resume-phases"></a><a name="bkmk_suspend"></a> Pausa och återuppta faser 

Du kan pausa eller återuppta en stegvis distribution manuellt. Du kan till exempel skapa en stegvis distribution för en aktivitetssekvens. När du övervakar fasen i din pilot grupp, märker du ett stort antal felaktiga försök. Du inaktiverar stegvis distribution för att stoppa ytterligare enheter från att köra aktivitetssekvensen. När du har löst problemet återupptar du den stegvisa distributionen för att fortsätta med distributionen. 

1. Hur du startar den här åtgärden varierar beroende på typ av distribuerad program vara:  

    - **Program** (endast i version 1806 eller senare): gå till arbets ytan **program varu bibliotek** , expandera **program hantering**och välj **program**.   

    - **Program uppdatering** (endast i version 1810 eller senare): gå till arbets ytan **program varu bibliotek** och välj en av följande noder:    
        - Programuppdateringar  
            - **Alla program uppdateringar**  
            - **Program uppdaterings grupper**   
        - Windows 10-underhåll, **alla Windows 10-uppdateringar**  
        - Office 365-klient hantering, **office 365-uppdateringar**  

    - **Aktivitetssekvens**: gå till arbets ytan **program varu bibliotek** , expandera **operativ system**och välj **aktivitetssekvenser**. Välj en befintlig aktivitetssekvens och klicka sedan på **skapa stegvis distribution** i menyfliksområdet.  

2. Välj program varan med den stegvisa distributionen.  

3. I informations fönstret växlar du till fliken stegvisa **distributioner** .  

4. Välj fasen stegvis distribution och klicka på **pausa** eller **återuppta** i menyfliksområdet. 

> [!NOTE]
> Från och med den 21 april 2020 kommer Office 365 ProPlus att byta namn till **Microsoft 365 appar för företag**. Mer information finns i [namn ändring för Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). Du kanske fortfarande ser det gamla namnet i Configuration Manager-produkten och dokumentationen medan-konsolen uppdateras. 

<!-- Removed for 1806, need to clarify behavior with engineering
When you suspend a phased deployment, it sets the available and deadline times on the active deployments to a future time. When you resume, it generates a new schedule based on when you resume the phased deployment. The new schedule helps to avoid problems if you resume after the original deadline. For example, the initial schedule has the required deadline seven days after the deployment is available. You suspend it on the second day. If you aren't ready to resume it until day eight, you don't want the deployment to be immediately past the deadline. So it generates a new deadline starting from when you resume the phased deployment on day eight. 
-->


## <a name="monitor"></a><a name="bkmk_monitor"></a> Övervakningsprogrammet
<!--1358577-->
Från och med version 1902 har stegvisa distributioner en egen dedikerad övervaknings nod, vilket gör det enklare att identifiera stegvisa distributioner som du har skapat och navigera till vyn övervakning av stegvis distribution. I arbets ytan **övervakning** väljer du stegvisa **distributioner**och dubbelklickar sedan på en av de stegvisa distributionerna för att se statusen. <!--3555949-->

I Configuration Manager 1806 och 1810 kan du se den inbyggda övervaknings miljön för stegvisa distributioner. Välj en stegvis distribution i noden **distributioner** på arbets ytan **övervakning** och klicka sedan på status för stegvis **distribution** i menyfliksområdet.

![Status instrument panel för stegvis distribution visar status för två faser](media/1358577-phased-deployment-status.png)

Den här instrument panelen visar följande information för varje fas i distributionen:  

- **Totalt antal enheter** eller **totala resurser**: hur många enheter som är riktade till den här fasen.  

- **Status**: aktuell status för den här fasen. Varje fas kan vara i något av följande tillstånd:  

    - **Distributionen har skapats**: den stegvisa distributionen skapade en distribution av program varan till samlingen för den här fasen. Klienterna är aktivt riktade mot den här program varan.  

    - **Väntar**: den föregående fasen har ännu inte nått kraven för lyckad distribution för att fortsätta till den här fasen.  

    - **Pausad**: en administratör pausade distributionen.  

- **Förlopp**: de färgkodade distributions tillstånden från klienter. Till exempel: lyckades, pågår, fel, kraven är inte uppfyllda och okänd. 

#### <a name="success-criteria-tile"></a>Panelen klart kriterium

Använd List rutan **Välj fas** om du vill ändra visningen av panelen **slutförda kriterier** . Den här panelen jämför **fas målet** med distributionens aktuella kompatibilitet. Med standardinställningarna är fas målet 95%. Det här värdet innebär att distributionen behöver en 95%-kompatibilitet för att gå vidare till nästa fas.

I exemplet är fas målet 65% och det aktuella efterlevnaden är 66,7%. Den stegvisa distributionen flyttades automatiskt till den andra fasen, eftersom den första fasen uppfyller framgångs villkoren.  

   ![Exempel panelen krav villkor från status för stegvis distribution där målet är 65%](media/pod-status-success-criteria-tile.png)

Fas målet är detsamma som **procent andelen lyckade distributioner** i fas inställningarna för *Nästa* fas. För den stegvisa distributionen för att starta nästa fas definierar den andra fasen villkoren för att lyckas med den första fasen. Så här visar du den här inställningen: 

1. Gå till det stegvisa distributions objekt i program varan och öppna de stegvisa distributions egenskaperna.  

2. Växla till fliken **faser** . Välj **fas 2** och klicka på **Visa**.  

3. I Fönstret Egenskaper fas växlar du till fliken **fas inställningar** .  

4. Visa värdet för **slutförd distribution i procent** i *villkoren för att lyckas med föregående fas* grupp.  

Till exempel är följande egenskaper för samma fas som panelen efterföljande villkor som visas ovan där kriterierna är 65%:  
![Fliken fas inställningar i fas egenskaper](media/phase-properties-phase-settings.png)

