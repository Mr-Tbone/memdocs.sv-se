---
title: Använd underhålls fönster
titleSuffix: Configuration Manager
description: Använd samlingar och underhålls fönster för att effektivt hantera klienter i Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4564ebcb-41a8-4eb0-afdb-2e1f0795cfa2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6c2128c9e26137c268577e68e5ee12e3a71f8513
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714446"
---
# <a name="how-to-use-maintenance-windows-in-configuration-manager"></a>Använda underhålls perioder i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Med underhålls perioder kan du definiera en tid när Configuration Manager åtgärder kan utföras på en enhets samling. Du kan använda underhålls perioder för att se till att klient konfigurations ändringar sker under perioder som inte påverkar produktiviteten. Från och med Configuration Manager version 1806 kan användarna se när nästa underhålls fönster är från fliken **installations status** i **Software Center**. <!--1358131-->

 Följande åtgärder har stöd för underhålls perioder:  

- Programdistributioner  

- Distribution av programuppdateringar  

- Distribution och utvärdering av kompatibilitetsinställningar  

- Distribution av operativsystem  

- Aktivitetssekvensdistribution  

  Konfigurera underhålls fönster med ett start datum, en start-och slut tid samt ett upprepnings mönster. Den maximala varaktigheten för ett fönster måste vara mindre än 24 timmar. Omstarter av datorn som orsakas av en distribution tillåts som standard inte utanför en underhålls period, men du kan åsidosätta standardvärdet. Underhålls perioder påverkar bara den tidpunkt då distributions programmet körs. program som har kon figurer ATS för att laddas ned och köras lokalt kan ladda ned innehåll utanför fönstret.  

  När en klient dator är medlem i en enhets samling som har en underhålls period körs ett distributions program bara om den längsta tillåtna körnings tiden inte överskrider varaktigheten som har kon figurer ATS för fönstret. Om programmet inte kan köras genereras en avisering och distributionen körs igen under nästa schemalagda underhållsperiod som har tillgänglig tid.  

## <a name="using-multiple-maintenance-windows"></a>Använda flera underhållsperioder  
 När en klient dator är medlem i flera enhets samlingar som har underhålls perioder gäller följande regler:  

- Om underhålls Fönstren inte överlappar hanteras de som två oberoende underhålls perioder.  

- Om underhålls perioderna överlappar varandra behandlas de som en enda underhålls period som omfattar den tids period som täcks av båda underhålls Fönstren. Om till exempel två Windows, varje timme i varaktighet överlappar 30 minuter, blir den effektiva tiden för underhålls perioden 90 minuter.  

  När en användare initierar en programinstallation från Software Center installeras programmet direkt, oavsett eventuella underhålls fönster.  

  Om en programdistribution som är **obligatorisk** når installationens tidsgräns under timmarna utanför arbetstid som konfigurerats av användaren i Software Center så installeras programmet. 

### <a name="how-to-configure-maintenance-windows"></a>Konfigurera underhållsperioder  

1.  I Configuration Manager-konsolen väljer du **till gångar och efterlevnad**>  **enhets samlingar**.  

3.  I listan **enhets samlingar** väljer du en samling. Du kan inte skapa underhålls perioder för samlingen **alla system** .  

4.  På fliken **Start** går du till gruppen **Egenskaper** och väljer **Egenskaper**.  

5.  På fliken **underhålls fönster** i dialog rutan ** &lt;egenskaper\> för samlings namn** klickar du på ikonen **ny** .  

6.  Slutför dialog ** &lt;rutan\> nytt schema** .  

7.  Välj i list rutan **Använd det här schemat till** .  

8.  Välj **OK** och Stäng dialog rutan ** &lt;egenskaper för\> samlings namn** .  
 
## <a name="using-powershell"></a><a name="bkmk_powershell"></a>Använda PowerShell

PowerShell kan användas för att konfigurera underhålls perioder.  Mer information finns i:

* [Set-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmmaintenancewindow)
* [Get-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmmaintenancewindow)
* [New-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmmaintenancewindow)
* [Remove-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmmaintenancewindow)
