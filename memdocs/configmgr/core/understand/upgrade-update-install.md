---
title: Om uppgradering, uppdatering och installation
titleSuffix: Configuration Manager
description: Lär dig skillnaden mellan villkoren för installation, uppdatering och uppgradering när du hanterar Configuration Manager infrastruktur.
ms.date: 04/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 17fab17f-304d-4f6a-87c7-30ab4f5521ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5af92990a0158172a441b052cdc2210e98fda9d5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722601"
---
# <a name="about-upgrade-update-and-install-for-site-and-hierarchy-infrastructure"></a>Om att uppgradera, uppdatera och installera för plats- och hierarkiinfrastruktur

*Gäller för: Configuration Manager (aktuell gren)*

När du hanterar Configuration Manager platser och hierarki-infrastruktur, används villkoren *Uppgradera*, *Uppdatera*och *Installera* för att beskriva tre olika begrepp.

## <a name="upgrade"></a>Uppgradera

*Uppgradering* eller *uppgradering på plats*används för att konvertera din Configuration Manager 2012-plats eller hierarki till en som kör Configuration Manager aktuella grenen.

När du uppgraderar System Center 2012 Configuration Manager för att Configuration Manager aktuella grenen fortsätter du att använda samma servrar som värd för dina platser och plats servrar och du behåller dina befintliga data och konfigurationer för Configuration Manager.  Detta skiljer sig från [migrering](../migration/migrate-data-between-hierarchies.md) , vilket är ett sätt att behålla dina konfigurationer och data om hanterade enheter när du använder nya Configuration Manager aktuella avdelnings webbplatser som är installerade på ny maskin vara.

Mer information finns i [Uppgradera till Configuration Manager](../servers/deploy/install/upgrade-to-configuration-manager.md).



## <a name="update"></a>Uppdatera
*Uppdatering* används för att installera uppdateringar i konsolen för Configuration Manager och för out-of-band-uppdateringar som inte kan levereras från Configuration Manager-konsolen. Uppdateringar i konsolen kan ändra versionen av din Current Branch plats (eller Technical Preview-webbplatsen) så att den kör en senare version. Om din webbplats exempelvis kör version 1806, kan du installera en uppdatering för version 1810. Uppdateringar kan även installera korrigeringar för ett känt problem, utan att ändra plats versionen.      

Uppdateringar lägger normalt till säkerhets korrigeringar, kvalitets förbättringar och nya funktioner i din befintliga distribution. Om du använder den tekniska förhands gransknings grenen kan en uppdatering installera en nyare version av den tekniska för hands versionen.
- Du väljer när du vill installera uppdateringen i konsolen, som börjar på den översta nivån i hierarkin.
- Du kan installera alla uppdateringar som är tillgängliga i-konsolen. Om din webbplats exempelvis kör version 1802 och både 1806 och 1810 erbjuds, bör du överväga att installera version 1810 eftersom varje version innehåller de funktioner som först gjorde tillgängliga i tidigare utgivna versioner.
- När en ny uppdatering har slutfört installationen på platsen på den översta nivån, startar underordnade primära platser automatiskt processen att uppdatera. Du kan dock ange [service fönster](../servers/manage/service-windows.md) för att kontrol lera uppdateringens tids inställning.
- Sekundära platser installerar inte automatiskt uppdateringar. I stället startar du uppdateringen manuellt från Configuration Manager-konsolen.

Mer information finns i [uppdateringar för Configuration Manager](../servers/manage/updates.md)och [teknisk för hands version för Configuration Manager](../get-started/technical-preview.md).



## <a name="install"></a>Installera
*Installera* används när du skapar en ny Configuration Manager-hierarki från grunden eller lägger till ytterligare platser i en befintlig hierarki.  

När du installerar en ny primär plats eller en central administrations plats beror platsen för setup. exe och relaterade källfiler som du använder på ditt installations scenario.

Mer information finns i [förbereda för att installera platser](../servers/deploy/install/prepare-to-install-sites.md).
