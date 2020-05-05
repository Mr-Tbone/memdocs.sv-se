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
ms.openlocfilehash: cc7eb1a8ba721545bdee50d45887ab9d3aa8e952
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721012"
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

-   Använd dokumentationen för din version av SQL Server för att komma igång med hur du flyttar en användar databas. Om du till exempel använder SQL Server 2014, se [Flytta användar databaser](https://technet.microsoft.com/library/ms345483\(v=sql.120\).aspx) på TechNet.  

-   När du har slutfört flyttningen av databas filen startar du om **SMS_EXECUTIVE** -tjänsten på Configuration Manager plats Server.  
