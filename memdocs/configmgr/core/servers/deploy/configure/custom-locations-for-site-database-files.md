---
title: Anpassade platser för databas fil
titleSuffix: Configuration Manager
description: Lär dig hur du anger anpassade platser för SQL Server databasfiler.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 500a9aa6-68aa-44eb-bf49-350c1314a697
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d3f01e54ba196ee9c27295d8f970a7dbe352f63f
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906181"
---
# <a name="custom-locations-for-configuration-manager-site-database-files"></a>Anpassade platser för Configuration Manager plats databasens filer

*Gäller för: Configuration Manager (aktuell gren)*

 Configuration Manager stöder anpassade platser för SQL Server databasfiler.  

> [!NOTE]  
>  Alternativet för att ange fil platser som inte är standard är inte tillgängligt när du använder ett SQL Server-kluster.  

 **Under installationen** av en ny primär plats eller Central administrations plats kan du:  

-   **Ange fil platser som inte är standard för plats databasen**: Configuration Manager installations programmet skapar sedan plats databasen med hjälp av dessa platser.  

-   **Ange användningen av en i förväg skapade SQL Server databas som använder anpassade fil platser**: Configuration Manager-installationen använder sedan den tidigare skapade databasen och de förkonfigurerade fil platserna.  

**Efter installationen**kan du ändra platsen för plats databasens filer. Detta kräver att du stoppar platsen och redigerar fil platsen i SQL Server:  

-   Stoppa tjänsten **SMS_EXECUTIVE** på Configuration Manager plats Server.  

-   Mer information om hur du flyttar en användar databas finns i [Flytta användar databaser](https://docs.microsoft.com/sql/relational-databases/databases/move-user-databases?view=sql-server-2014).  

-   När du har slutfört flyttningen av databas filen startar du om **SMS_EXECUTIVE** -tjänsten på Configuration Manager plats Server.  
