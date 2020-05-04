---
title: Säkerhet och sekretess för energisparfunktioner
titleSuffix: Configuration Manager
description: Hämta information om säkerhet och sekretess för energispar funktioner i Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 469ff35f-59a1-484d-902b-107dd6070baf
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: c019faee1ffa035bde626778bb15b8f5feabc243
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715181"
---
# <a name="security-and-privacy-for-power-management-in-configuration-manager"></a>Säkerhet och sekretess för energispar funktioner i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Det här avsnittet innehåller information om säkerhet och sekretess för energispar funktioner i Configuration Manager.  

## <a name="security-best-practices-for-power-management"></a>Rekommenderade säkerhetsmetoder för energisparfunktioner  
 Det finns inga säkerhetsrelaterade metodtips för energisparfunktioner.  

## <a name="privacy-information-for-power-management"></a>Sekretessinformation för energisparfunktioner  
 Energisparfunktioner använder funktioner som är inbyggd i Windows för att övervaka energiförbrukningen och tillämpa energiinställningar på datorer under kontorstid och utanför arbetstid. Configuration Manager samlar in information om energi användningen från datorer, som innehåller information om när en användare använder en dator. Även om Configuration Manager övervakar energi förbrukningen för en samling snarare än för varje dator kan en samling innehålla en enda dator. Energisparfunktioner är inte aktiverade som standard och måste konfigureras av en administratör.  

 Informationen om energi förbrukningen lagras i Configuration Manager-databasen och skickas inte till Microsoft. Detaljerad information lagras i databasen i 31 dagar och sammanfattad information sparas i 13 månader. Du kan inte konfigurera borttagningsintervallet.  

 Innan du konfigurerar energisparfunktionerna bör du tänka igenom dina sekretesskrav.  
