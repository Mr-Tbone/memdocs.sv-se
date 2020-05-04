---
title: Uppdatera och dra tillbaka program
titleSuffix: Configuration Manager
description: Ändra, Ersätt eller avinstallera distribuerade program med hjälp av Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 68ac8a07-8e54-4a3c-91e3-e50dc1cabf5d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7770f1db0e311186a908890dc339401ed3cbeb4b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710533"
---
# <a name="update-and-retire-applications-with-configuration-manager"></a>Uppdatera och dra tillbaka program med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*


Det är troligt att du vill göra ändringar i ett program, avinstallera ett program eller ersätta ett redan distribuerat program med ett nytt program. Configuration Manager ger dig dessa funktioner, som hjälper dig att uppdatera och dra tillbaka program:  

- **Omarbeta program**. När du gör ändringar i ett program eller en distributions typ, så behåller Configuration Manager en historik över ändringarna. Du kan återställa programmet till en tidigare version när som helst. Du kan också visa dess egenskaper, återställa en tidigare revision av ett program eller ta bort en gammal revision.  

  Mer information finns i [program revisioner](revise-and-supersede-applications.md#application-revisions).  

- **Ersätt program**. Du kan uppgradera eller ersätta befintliga program med hjälp av en ersättande relation. När du ersätter ett program kan du ange en ny distributions typ som ersätter det ersatta programmets distributions typ. Du kan också ange om du vill uppgradera eller avinstallera det ersatta programmet innan det ersättande programmet installeras.  

  Mer information finns i [program ersättning](revise-and-supersede-applications.md#application-supersedence).  

- **Avinstallera program**. Configuration Manager gör det enkelt att avinstallera ett program. Detta kan utföras tyst, utan att det sker någon åtgärd från program-eller enhets användaren.  

  Mer information finns i [Avinstallera program](uninstall-applications.md).  
