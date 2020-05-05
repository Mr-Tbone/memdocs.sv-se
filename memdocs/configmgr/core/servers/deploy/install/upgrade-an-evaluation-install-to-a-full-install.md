---
title: Installation av uppgraderings utvärdering
titleSuffix: Configuration Manager
description: Lär dig hur du uppgraderar en utvärderings installation till en fullständig installation av Configuration Manager.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9a32f5a3-9917-434f-9811-106170f404be
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a8a42b2538ff1baaceb6895d371081ac2a444c5f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718002"
---
# <a name="upgrade-an-evaluation-installation-of-configuration-manager-to-a-full-installation"></a>Uppgradera en utvärderings installation av Configuration Manager till en fullständig installation

*Gäller för: Configuration Manager (aktuell gren)*

Om du har installerat Configuration Manager som en utvärderings version, efter 180 dagar, blir Configuration Manager-konsolen skrivskyddad tills du aktiverar produkten från sidan **plats underhåll** i installations programmet. När som helst före eller efter 180-dagars perioden har du möjlighet att uppgradera en utvärderings installation till en fullständig installation.  

> [!NOTE]  
>  När du ansluter en Configuration Manager-konsol till en utvärderings installation av Configuration Manager visar konsolens namn List antalet dagar som återstår tills utvärderings installationen upphör att gälla. Antalet dagar uppdateras inte automatiskt och uppdateras bara när du skapar en ny anslutning till en plats.  

 Du kan uppgradera följande webbplatser som kör en utvärderings installation:  

-   Central administrationsplats  
-   Primär plats  

Eftersom sekundära platser inte behandlas som utvärderings installationer behöver du inte ändra en sekundär plats efter att den primära överordnade platsen har uppgraderats till en fullständig installation.  

Krav för att uppgradera en utvärderings version till en licensierad version:  

-   Du måste ha en giltig produkt som ska användas under uppgraderingen.  
-   Ditt konto måste ha **Administratörs** behörighet på den dator där platsen är installerad.  

### <a name="to-upgrade-an-evaluation-version-of-configuration-manager-to-a-licensed-version"></a>Uppgradera en utvärderings version av Configuration Manager till en licensierad version  

1.  På plats servern kör du **Setup. exe** (Configuration Manager installation) från Configuration Manager-installationsmappen (**%path%\BIN\X64**). Du måste köra kopian av installationen som finns på plats servern i mappen Configuration Manager eftersom alternativen för plats underhåll inte är tillgängliga när du kör installations programmet från installations mediet.  
2.  Välj **Nästa**på sidan **innan du börjar** .  
3.  På sidan **komma igång** väljer du **utför plats underhåll eller Återställ platsen**och väljer sedan **Nästa**.  
4.  På sidan **plats underhåll** väljer **du uppgradera utvärderings versionen till en licensierad utgåva**, anger en giltig produkt nyckel och väljer sedan **Nästa**.  
5.  På sidan **licens villkor för program vara från Microsoft** läser du igenom och godkänner licens villkoren och väljer sedan **Nästa**.  
6.  På sidan **konfiguration** väljer du **Stäng** för att slutföra guiden.  

    > [!NOTE]  
    >  Namn listen för en Configuration Manager-konsol som är ansluten till den plats som du uppgraderar kan indikera att platsen fortfarande är en utvärderings version tills du återansluter-konsolen till platsen.  
