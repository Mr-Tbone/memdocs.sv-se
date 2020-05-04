---
title: Fjärradministrera en Windows-dator
titleSuffix: Configuration Manager
description: Administrera en fjärran sluten Windows-klientdator med hjälp av Configuration Manager.
ms.date: 11/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3c9648c4-645e-4e47-ae10-2da817b8c83b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 801654b95470889d0b661315d40d3e00efa8e542
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715111"
---
# <a name="how-to-remotely-administer-a-windows-client-computer-by-using-configuration-manager"></a>Fjärradministrera en Windows-klientdator med hjälp av Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)* Med Configuration Manager kan du ansluta till klient datorer med **Configuration Manager fjärr styrning**. Innan du börjar använda fjärr styrning bör du kontrol lera informationen i följande artiklar:  

-   [Krav för fjärrstyrning](prerequisites-for-remote-control.md)  

-   [Konfigurera fjärrstyrning](configuring-remote-control.md)  

Här är tre sätt att starta visaren för fjärr styrning:  

-   I Configuration Manager-konsolen.  

-   I kommando tolken i Windows.  

-   Från **Start** -menyn i Windows på en dator som kör Configuration Manager-konsolen, i program gruppen **Microsoft System Center** .  

## <a name="to-remotely-administer-a-client-computer-from-the-configuration-manager-console"></a>Så här fjärradministrerar du en klientdator från Configuration Manager-konsolen  

1.  I Configuration Manager-konsolen väljer du **till gångar och efterlevnad** > **enheter** eller **enhets samlingar**.  

3.  Välj den dator som du vill fjärradministrera och på fliken **Start** i gruppen **enhet** väljer du **Starta** > **fjärr styrning**.  

    > [!IMPORTANT]  
    >  Om klientinställningen **Fråga användaren om Fjärrstyrning-behörighet** har värdet **Sant**initieras inte anslutningen förrän användaren på fjärrdatorn accepterar förfrågan om fjärrstyrning. Mer information finns i [Konfigurera fjärr styrning](configuring-remote-control.md).  

4.  När fönstret **Configuration Manager-fjärrstyrning** har öppnats kan du fjärradministrera klientdatorn. Konfigurera anslutningen med hjälp av följande alternativ.  

    > [!NOTE]  
    >  Om datorn som du ansluter till har flera bildskärmar visas visningen från alla Övervakare i fönstret fjärr styrning.  

    -   **Fil**
        - **Anslut** – Anslut till en annan dator. Det här alternativet är inte tillgängligt om en fjärrstyrningssession är aktiv.  
        -   **Koppla** från – kopplar från den aktiva fjärrstyrningssession, men stänger inte fönstret **Configuration Manager fjärr styrning** .  
        - **Exit** -kopplar från den aktiva fjärrstyrningssession och stänger fönstret **Configuration Manager fjärr styrning** .  

        > [!NOTE]  
        >  När du kopplar från en fjärrstyrningssession raderas innehållet i Urklipp i Windows på den dator som du visar.


    - **Vy**
      - **Färgdjup** – Välj antingen 16 bitar eller 32 bitar per bild punkt.
      -  **Full skärm** – maximerar fönstret **Configuration Manager fjärr styrning** . Du avslutar helskärmsläge genom att trycka på Ctrl+Alt+Break.  
      - **Optimera för anslutning med låg bandbredd** – Välj det här alternativet om anslutningen har låg bandbredd.
      - **Hur**
        - **Alla skärmar** – läggs till i Configuration Manager 1902. Om datorn som du ansluter till har flera bildskärmar visas visningen från alla Övervakare i fönstret fjärr styrning. **Alla skärmar** är den enda vyn för datorer med flera övervakare före 1902.
        -  **Första skärmen** – tillagt i Configuration Manager 1902. Den *första skärmen* är längst upp och längst till vänster som visas i visnings inställningarna för Windows. Du kan inte välja en speciell skärm. När du växlar konfigurationen av visnings programmet ansluter du fjärrsessionen igen. Visnings programmet sparar inställningarna för framtida anslutningar.
        -  **Skala för att passa** – skalar visningen av fjärrdatorn så att den passar storleken på **Configuration Manager fjärr styrnings** fönstret.
        - **Statusfält** – växlar visning av statusfältet för **Configuration Manager fjärr styrnings** fönster.  

       > [!NOTE]  
       >  Visnings programmet sparar inställningarna för framtida anslutningar.

    -   **Åtgärd**
        - **Skicka CTRL + ALT + del** – skickar en tangentkombination för CTRL + ALT + del till fjärrdatorn. 
        - **Aktivera delning av Urklipp** – låter dig kopiera och klistra in objekt till och från fjärrdatorn. Om du ändrar det här värdet måste du starta om fjärrstyrningssessionen innan ändringen börjar gälla.   
          - Om du inte vill att delning av Urklipp ska vara aktiverat i Configuration Manager-konsolen anger du värdet för register nyckeln **HKEY_CURRENT_USER \Software\microsoft\configmgr10\remote Control\Clipboard delning** till **0**på datorn som kör-konsolen.
        - **Aktivera tangent bords översättning** – översätter tangentbordslayouten för datorn som kör-konsolen till den anslutna enhetens layout.
        - **Lås fjärrtangentbord och mus** – låser fjärrtangentbordet och musen så att användaren inte kan använda fjärrdatorn.  

    -   **Hjälp**
        - **Om fjärr styrning** – visar den aktuella versionen av visnings programmet.  

5.  Användare på fjärrdatorn kan visa mer information om fjärrstyrningssession när de klickar på ikonen Configuration Manager **fjärr styrning** . Ikonen är i meddelande fältet i Windows eller ikonen i sessionstillståndet för fjärr styrning.  

## <a name="to-start-the-remote-control-viewer-from-the-windows-command-line"></a>Så här startar du visaren för fjärrstyrning från kommandoraden i Windows  

-   I kommando tolken i Windows skriver du _<Configuration Manager installationsmapp\>_**\AdminConsole\Bin\i386\CmRcViewer.exe**  

CmRcViewer.exe stöder följande kommandoradsalternativ:  

- *Adress* – anger NetBIOS-namnet, det fullständigt kvalificerade domän namnet (FQDN) eller IP-adressen för den klient dator som du vill ansluta till.
- *Plats Server namn* – anger namnet på den Configuration Manager plats Server till vilken du vill skicka status meddelanden som är relaterade till fjärrstyrningssession.
- **/?** – Visar kommando rads alternativen för visaren för fjärr styrning.  
     
**Exempel: CmRcViewer. exe** *<adress\> \Site-* * < \\servernamn>* 

> [!NOTE]  
> Visnings programmet för fjärr styrning stöds på alla operativ system som stöds för Configuration Manager-konsolen. Mer information finns i [konfigurationer som stöds för Configuration Manager konsoler](../../../plan-design/configs/supported-operating-systems-consoles.md) och [krav för fjärr styrning](prerequisites-for-remote-control.md).

## <a name="next-steps"></a>Nästa steg

[Granska användning av fjärr styrning](audit-remote-control-usage.md)
