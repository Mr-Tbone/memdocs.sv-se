---
title: Internationell support
titleSuffix: Configuration Manager
description: Konfigurera Configuration Manager för att uppfylla särskilda internationella krav.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 46dd9cb2-a812-4b6a-a747-b840f92fef8b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 05e90466ec3ee9529e4eb770839347ad7ac94447
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720942"
---
# <a name="international-support-in-configuration-manager"></a>Internationellt stöd i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Följande avsnitt innehåller teknisk information som hjälper dig att göra Configuration Manager kompatibla med särskilda internationella krav.  

## <a name="gb18030-requirements"></a>GB18030-krav  
 Configuration Manager uppfyller de standarder som definieras i GB18030 så att du kan använda Configuration Manager i Kina. En Configuration Manager distribution måste ha följande konfigurationer för att uppfylla GB18030-kraven:  

-   Varje plats serverdator och SQL Server dator som du använder med Configuration Manager måste använda ett kinesiskt operativ system.  

-   Varje platsdatabas och instans av SQL Server i hierarkin måste använda samma sortering och måste vara någon av följande:  

    -   Chinese_Simplified_Pinyin_100_CI_AI  

    -   Chinese_Simplified_Stroke_Order_100_CI_AI  

    > [!NOTE]  
    >  De här databas sorteringarna är ett undantag till de krav som anges i [stöd för SQL Server versioner för Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md).  

-   Du måste placera en fil med namnet **GB18030.SMS** i systemvolymens rotmapp för varje platsserverdator i hierarkin. Filen innehåller inga data och kan vara en tom textfil som döps för att uppfylla det här kravet.  
