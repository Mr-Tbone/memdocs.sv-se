---
title: Hantera frågor
titleSuffix: Configuration Manager
description: Lär dig hur du hanterar dina frågor. Innehåller en tabell för detaljerad referens.
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e562e2a0-8df8-4952-952f-e8c38461c612
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 37050a3a96b732df3f56269592e049077008ab2b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713753"
---
# <a name="how-to-manage-queries-in-configuration-manager"></a>Hantera frågor i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Den här artikeln kan hjälpa dig att hantera frågor i Configuration Manager.  

 Information om hur du skapar frågor finns i [så här skapar du frågor](../../../core/servers/manage/create-queries.md).  

## <a name="manage-queries"></a>Hantera frågor
 Välj **Frågor** på arbetsytan **Övervakning**, välj den fråga som du vill hantera och välj sedan en hanteringsaktivitet.  

 Följande tabell innehåller information om hanterings aktiviteterna.  

|Hanteringsaktivitet|Information| 
|---------------------|-------------|
|**Fungerar**|Kör den valda frågan och visar resultatet i Configuration Manager-konsolen.|
|**Installera klient**|Öppnar **guiden Installera klient**där du kan installera Configuration Manager-klienten på datorer som returneras av den valda frågan.<br /><br /> Det här alternativet är inte tillgängligt för frågor som returnerar mobila enheter, användare eller användar grupper. <br /><br /> Mer information om hur du installerar Configuration Manager-klienter med push-installation av klienter finns i [Distribuera klienter till Windows-datorer](../../clients/deploy/deploy-clients-to-windows-computers.md).| 
|**Exportera**|Öppnar **guiden Exportera objekt**. Med den här guiden kan du exportera frågan till en Managed Object Format-fil (MOF) som du sedan kan importera på en annan plats.
|**Flytta**|Öppnar dialog rutan **Flytta markerade objekt** . I den här dialog rutan kan du flytta den valda frågan till en mapp som du tidigare skapat under noden **frågor** .|

## <a name="next-steps"></a>Nästa steg 
 [Skapa frågor](../../../core/servers/manage/create-queries.md)
