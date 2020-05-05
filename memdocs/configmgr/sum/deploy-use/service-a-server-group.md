---
title: Tjänster för servergrupp
titleSuffix: Configuration Manager
description: Configuration Manager-konsolen innehåller aviseringar och statusar för att övervaka uppdateringar och efterlevnad.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/01/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 304a83ea-0f72-437d-9688-2e6e0c7526dd
ms.openlocfilehash: 7d6d8bef145e14547e5e6a726a93cb9470b94afd
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724330"
---
# <a name="service-a-server-group"></a>Tjänster för servergrupp

*Gäller för: Configuration Manager (aktuell gren)*

>[!IMPORTANT]
> - Från och med Configuration Manager version 2002 har Server grupper ersatts av Orchestration-grupper. Mer information finns i [Orchestration-grupper](orchestration-groups.md).
> - För hands versions funktioner finns funktioner som finns i Current Branch för tidig testning i en produktions miljö. Dessa funktioner stöds fullt ut men är fortfarande aktiva och kan ta emot ändringar tills de flyttas från för hands versions kategorin. Du måste aktivera den här funktionen för att den ska vara tillgänglig. Mer information finns i [Använda förhandsversionsfunktioner från uppdateringar](../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease).

Från och med Configuration Manager version 1606 kan du konfigurera server grupps inställningar för en samling för att definiera hur många, procent andel eller i vilken ordning datorer i samlingen ska installera program uppdateringar. Du kan också konfigurera PowerShell-skript för för distribution och efter distribution för att köra anpassade åtgärder.

När du distribuerar program uppdateringar till en samling som har inställningar för Server grupp konfigurerad, fastställer Configuration Manager hur många datorer i samlingen som kan installera program uppdateringarna vid en angiven tidpunkt och gör samma antal tillgängliga distributions lås. Installationen av program uppdateringen startar endast på datorer som får ett distributions lås. När ett distributions lås är tillgängligt hämtar en dator distributions låset, installerar program uppdateringarna och släpper sedan distributions låset när installationen av program uppdateringarna har slutförts. Sedan blir distributions låset tillgängligt för andra datorer. Om en dator inte kan släppa ett distributions lås kan du manuellt släppa alla Server grupps distributions lås för samlingen.

>[!IMPORTANT]
>Alla datorer i samlingen måste tilldelas samma plats.

#### <a name="to-create-a-collection-for-a-server-group"></a>Så här skapar du en samling för en Server grupp  
Inställningarna för Server gruppen konfigureras i egenskaperna för en enhets samling. Om du vill underhålla en Server grupp måste alla medlemmar i samlingen tilldelas samma plats. Använd följande steg för att skapa en samling och konfigurera server grupps inställningarna:
1.  [Skapa en enhets samling](../../core/clients/manage/collections/create-collections.md) som innehåller datorerna i Server gruppen.  

2.  I arbets ytan **till gångar och efterlevnad** klickar du på **enhets samlingar**, högerklickar på den samling som innehåller datorerna i Server gruppen och klickar sedan på **Egenskaper**.  

3.  På fliken **Allmänt** väljer du **alla enheter tillhör samma server grupp**och klickar sedan på **Inställningar**.  

4.  På sidan **Inställningar för Server grupp** anger du en av följande inställningar:  

    -   **Tillåt att en procent andel av datorerna uppdateras samtidigt**: anger att endast en viss procent andel av klienterna uppdateras vid ett och samma tillfälle. Om samlingen till exempel har 10 klienter och samlingen har kon figurer ATS för att uppdatera 30% av klienterna samtidigt, kommer bara 3 klienter att installera program uppdateringar vid en angiven tidpunkt.  

    -   **Tillåt att ett antal datorer uppdateras samtidigt**: anger att endast ett visst antal klienter uppdateras vid ett och samma tillfälle.  

    -   **Ange underhålls ordningen**: anger att klienterna i samlingen ska uppdateras en i taget i den ordning som du konfigurerar. En klient kommer bara att installera program uppdateringar när klienten är före den i listan har installerat program uppdateringarna.  

5.  Ange om du vill använda ett skript för för distribution (Node dränering) eller efter distribution (Node Resume).  

    > [!WARNING]
    > Anpassade skript signeras inte av Microsoft. Det är ditt ansvar att upprätthålla integriteten för dessa skript.

    > [!TIP]  
    > Följande är exempel som du kan använda vid testning av skript för för distribution och efter distribution som skriver den aktuella tiden till en textfil:  
    >   
    >  **Före distribution**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\Windows\Temp\start.txt`  
    >   
    >  **Efter distributionen**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\Windows\Temp\end.txt`  

## <a name="deploy-software-updates-to-the-server-group-and-monitor-status"></a>Distribuera program uppdateringar till Server gruppen och övervaka status  
Du distribuerar program uppdateringar till Server grupps samlingen med hjälp av den vanliga distributions processen. När du har distribuerat program uppdateringarna kan du övervaka program uppdaterings distributionen i Configuration Manager-konsolen.
1.  [Distribuera program uppdateringar](manually-deploy-software-updates.md) till Server grupps samlingen.   

2.  [Övervaka program uppdaterings distributionen](monitor-software-updates.md). Förutom standardvyerna för övervakning av program uppdateringar visas en **väntande lås** status när en klient väntar på att program uppdateringarna ska installeras. Du kan granska filen UpdatesDeployment. log om du vill ha mer information.


## <a name="clear-the-deployment-locks-for-computers-in-a-server-group"></a>Rensa distributions lås för datorer i en Server grupp  
När en dator inte kan släppa ett distributions lås kan du manuellt släppa alla Server grupps distributions lås för samlingen. Rensa bara Lås när en distribution har fastnat i att uppdatera datorer i samlingen och det finns datorer som fortfarande inte är kompatibla.  
1.  Klicka på **enhets samlingar**på arbets ytan **till gångar och efterlevnad** och klicka på samlingen för att rensa distributions lås.  

2.  På fliken **Start** går du till gruppen **distribution** och klickar på **ta bort Server grupp distributions lås**. När klienterna har misslyckats med att installera program uppdateringarna och hindrar andra klienter från att installera sina program uppdateringar, kan distributions låsen rensas manuellt.  
