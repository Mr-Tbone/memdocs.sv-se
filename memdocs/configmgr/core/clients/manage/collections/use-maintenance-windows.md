---
title: Använd underhålls fönster
titleSuffix: Configuration Manager
description: Använd samlingar och underhålls fönster för att effektivt hantera klienter i Configuration Manager.
ms.date: 06/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4564ebcb-41a8-4eb0-afdb-2e1f0795cfa2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0b81599c6c5e4dda418b69c6e3c6d3b8cd144253
ms.sourcegitcommit: 92e6d2899b1cf986c29c532d0cd0555cad32bc0c
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2020
ms.locfileid: "84428540"
---
# <a name="how-to-use-maintenance-windows-in-configuration-manager"></a>Använda underhålls perioder i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Använd underhålls perioder för att definiera när Configuration Manager kan köra påverkan på uppgifter på enheter. Underhålls hjälp för Windows se till att klient konfigurations ändringar sker under tider som inte påverkar produktiviteten. I Software Center kan användarna se nästa underhålls period för enheten på fliken **installations status** . <!--1358131-->

Följande uppgifter stöder underhålls perioder:

- Program-och paket distributioner

- Distribution av programuppdateringar

- Distribution och utvärdering av kompatibilitetsinställningar

- Distributioner av OS och anpassad aktivitetssekvensdistribution

Konfigurera underhålls fönster med ett effektivt datum, en start-och slut tid och ett upprepnings mönster. Den maximala varaktigheten för ett fönster måste vara mindre än 24 timmar. Konsolen tillåter inte ett enda underhålls fönster längre än 24 timmar. Om du till exempel vill tillåta underhåll varje dag lördag och söndag skapar du 2 24-timmars underhålls fönster för varje dag.<!-- MEMDocs#310 -->

Omstarter av datorn som orsakas av en distribution tillåts som standard inte utanför en underhålls period, men du kan åsidosätta standardvärdet. Underhålls perioder påverkar bara den tidpunkt då distributionen körs. Distributioner som du konfigurerar för att ladda ned och köra lokalt kan ladda ned innehåll utanför fönstret.

När en klient är medlem i en enhets samling som har en underhålls period körs en distribution endast om den högsta tillåtna körnings tiden inte överskrider fönstrets varaktighet. Om distributionen inte kan köras genererar klienten en avisering. Sedan kör den om distributionen under nästa schemalagda underhålls period som har tillgänglig tid.

## <a name="multiple-maintenance-windows"></a>Flera underhålls fönster

När en klient dator är medlem i flera enhets samlingar som har underhålls perioder gäller följande regler:  

- Om underhålls Fönstren inte överlappar varandra behandlar klienten dem som två separata underhålls perioder.

- Om underhålls perioderna överlappar varandra behandlar klienten dem som ett enda fönster för hela tiden för båda Fönstren. Du kan till exempel skapa två underhålls fönster för en samling. Den första gäller från 6:00 till 7:00 och den andra är från 6:30 till 7:30. Eftersom de överlappar med 30 minuter är den effektiva varaktigheten för det kombinerade underhålls fönstret 90 minuter från 6:00 till 7:30.

När en användare installerar ett program från Software Center startas klienten direkt. Den prioriterar användarens avsikt över administratören.

Om en program distribution med ett **obligatoriskt** syfte når installations tids gränsen under den tid som en användare konfigurerar i Software Center, installerar-klienten programmet. Den prioriterar administratörens avsikt över användaren.

Som standard, med flera underhålls fönster, installerar klienten bara program uppdateringar under **program uppdaterings** typ Windows. Alla **distributions** underhålls fönster ignoreras, om de inte är den enda typen. Du kan konfigurera det här beteendet med följande klient inställning i gruppen **program uppdateringar** : **Aktivera installation av program uppdateringar i underhålls fönstret för alla distributioner när underhålls fönstret program uppdatering är tillgängligt**. Mer information finns i [om klient inställningar](../../deploy/about-client-settings.md#bkmk_SUMMaint).<!-- SCCMDocs#1317 -->

> [!NOTE]
> Den här inställningen gäller även för de underhålls fönster som du konfigurerar för att tillämpa på **aktivitetssekvenser**.<!-- SCCMDocs-pr #4596 -->
>
> Om klienten endast har ett fönster för **alla distributioner** , installerar det fortfarande program uppdateringar eller aktivitetssekvenser i fönstret.

## <a name="configure-maintenance-windows"></a>Konfigurera underhålls fönster

1. Gå till arbets ytan **till gångar och efterlevnad** i Configuration Manager-konsolen.

1. Välj noden **enhets samlingar** och välj sedan en samling.

    > [!NOTE]
    > Du kan inte skapa underhålls perioder för samlingen **alla system** .

1. Välj **Egenskaper**i gruppen **Egenskaper** på fliken **Start** i menyfliksområdet.

1. Växla till fliken **underhålls fönster** och välj ikonen **ny** .

    1. Ange ett **namn** för att unikt identifiera underhålls perioden för samlingen.

    1. Konfigurera **tids** inställningarna:

        - **Effektivt datum**: det datum då underhålls Fönstren startar. Standardvärdet är det aktuella datumet.

        - **Start** och **slut**: Start-och slut tiderna för underhålls perioden. Den beräknar **varaktigheten** för fönstret. Den minsta varaktigheten är fem minuter och det maximala värdet är 24 timmar. Standard varaktigheten är tre timmar från 01:00 till 04:00.

        - **UTC (Coordinated Universal Time)**: aktivera det här alternativet för att klienten ska kunna tolka start-och slut tiderna i UTC-tidszonen. För regional eller globalt distribuerade enheter i samma samling anger det här alternativet att underhålls perioden ska inträffa samtidigt på alla enheter i samlingen. Inaktivera det här alternativet för att klienten ska använda enhetens lokala tidszon. Det här alternativet är inaktiverat som standard.

    1. Konfigurera upprepnings mönstret. Standardvärdet är en gång per vecka på den aktuella dagen i veckan.

    1. **Använd det här schemat till**: som standard gäller fönstret för **alla distributioner**. Du kan välja antingen **program uppdateringar** eller **aktivitetssekvenser** för att styra vilka distributioner som körs under det här fönstret.

        > [!TIP]
        > Om du konfigurerar flera underhålls fönster av olika typer i samma samling, se till att du förstår klient beteendena. Mer information finns i [flera underhålls fönster](#multiple-maintenance-windows).

1. Välj **OK** för att spara och stänga fönstret.

Fliken **underhålls fönster** i egenskaperna för samlingen visar alla konfigurerade fönster.

## <a name="use-powershell"></a><a name="bkmk_powershell"></a>Använd PowerShell

PowerShell kan användas för att konfigurera underhålls perioder. Mer information finns i följande artiklar:

- [Get-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmmaintenancewindow?view=sccm-ps)
- [New-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmmaintenancewindow?view=sccm-ps)
- [Remove-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmmaintenancewindow?view=sccm-ps)
- [Set-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmmaintenancewindow?view=sccm-ps)
