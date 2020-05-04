---
title: Krav för samlingar
titleSuffix: Configuration Manager
description: Hämta krav för att använda samlingar i Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a53e4cf1-518a-4210-9c16-022c4261d2fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 313c3183cd6401390d743575ba513026a3e3f607
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714502"
---
# <a name="prerequisites-for-collections-in-configuration-manager"></a>Krav för samlingar i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Samlingar i Configuration Manager innehåller endast beroenden inom produkten.  

## <a name="configuration-manager-dependencies"></a>Beroenden i Configuration Manager  

|Beroende|Mer information|  
|----------------|----------------------|  
|Rapporteringstjänstpunkt|Platssystemrollen Reporting Services-plats måste installeras innan du kan köra rapporter för samlingar. Mer information finns i [Introduktion till rapportering](../../../servers/manage/introduction-to-reporting.md).|  
|Det krävs specifika säkerhetsbehörigheter för att hantera samlingar|Du måste ha följande säkerhetsbehörigheter för att hantera kompatibilitetsinställningar:<br /><br /> – Om du vill skapa och hantera samlingar: **skapa**, **ta bort**, **ändra**, **ändra mapp**, **Flytta objekt**, **läsa** och **läsa resurs** för objektet **samling** .<br /><br /> -För att hantera samlings inställningar: ändra insamlings **inställning** för objektet **samling** .<br /><br /> Behörigheten **Ändra mapp** krävs för alla insamlingsmappar, inklusive rotmappen.|  
