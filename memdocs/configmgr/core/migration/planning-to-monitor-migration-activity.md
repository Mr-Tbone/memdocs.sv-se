---
title: Övervaka migrering
titleSuffix: Configuration Manager
description: Lär dig hur du använder Configuration Manager-konsolen för att övervaka förloppet och framgången av migreringsjobb.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: fc731d3f-edd7-4049-b17b-653d6693a564
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f9d1766a374c7abd8b13f503c3c7a64e35a5ac2c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713004"
---
# <a name="planning-to-monitor-migration-activity-in-configuration-manager"></a>Planera övervakning av migreringen i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Med Configuration Manager kan du övervaka migreringen i Configuration Manager-konsolen som ansluts till målhierarkin. I Configuration Manager-konsolen på arbets ytan **Administration** kan du använda noden **migrering** för att övervaka förloppet och framgångs jobben. Du kan visa sammanfattnings information för varje migreringsjobb som identifierar objekt som har migrerats, de objekt som ännu inte har migrerats och antalet objekt som är exkluderade från ett migreringsjobb. Du kan också se information om eventuella migreringsåtgärder.  

## <a name="view-migration-progress"></a>Visa migreringens förlopp  
 Om du vill visa förloppet för ett migreringsjobb använder du någon av följande åtgärder:  

-   I arbets ytan **Administration** i Configuration Manager-konsolen expanderar du noden **migreringsjobb** , väljer ett migreringsjobb och väljer sedan **objekten på fliken jobb** .  

-   Använd Configuration Manager loggfiler för att granska migreringens förlopp eller för att identifiera eventuella problem. Migration Manager är den Configuration Manager processen som spårar migreringen och registrerar dessa i MIGMCTRL. log-filen i mappen ** \&lt;\>\\InstallationPath logs** på plats servern.  

    > [!NOTE]  
    >  Om ett migreringsjobb Miss lyckas granskar du informationen i MIGMCTRL. log-filen så snart som möjligt. Logg posterna för migrering läggs kontinuerligt till i filen och den gamla informationen skrivs över. Om posterna skrivs över kanske du inte kan identifiera om några problem som kan uppstå med de migrerade objekten relaterar till problem med migreringen. Migreringen loggas på platsen på\-den högsta nivån i hierarkin, oavsett vilken plats Configuration Manager-konsolen ansluter till när du konfigurerar migreringen.  

-   Använd Configuration Manager rapportering. Configuration Manager innehåller flera inbyggda\-rapporter för migrering, eller så kan du redigera rapporterna så att de passar dina behov. Mer information om Configuration Manager-rapporter finns i [Introduktion till rapportering](../servers/manage/introduction-to-reporting.md).  
