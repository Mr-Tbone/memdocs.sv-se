---
title: Krav för energisparfunktioner
titleSuffix: Configuration Manager
description: Hämta kraven för energispar funktioner i Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9c062f13-3c1f-4621-9cae-de0e322aa03f
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: a816d333d96dba6cb1c38f6499ccac78e2db8a3c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715188"
---
# <a name="prerequisites-for-power-management-in-configuration-manager"></a>Krav för energispar funktioner i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Energispar funktioner i Configuration Manager har externa beroenden och beroenden inom produkten.  

## <a name="dependencies-external-to-configuration-manager"></a>Beroenden utanför Configuration Manager  
 I följande tabell visas de beroenden som är externa för att Configuration Manager för användning av energispar funktioner.  

|Beroende|Mer information|  
|----------------|----------------------|  
|Klientdatorer måste kunna stödja de energisparfunktioner som krävs.|För att kunna använda alla energisparfunktioner måste klientdatorerna ha stöd för viloläge och strömsparläge samt aktivering från dessa lägen. Du kan använda rapporten **Energisparfunktioner** för att ta reda på om datorerna har stöd för de här åtgärderna. Mer information finns i [rapporten energi funktioner](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Capabilites) i artikeln [så här övervakar och planerar du för energispar](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md)funktioner.|  

## <a name="configuration-manager-dependencies"></a>Beroenden i Configuration Manager  
 I följande tabell visas beroenden i Configuration Manager för användning av energispar funktioner.  

|Beroende|Mer information|  
|----------------|----------------------|  
|Energisparfunktioner måste vara aktiverat för när du skapar och övervakar energischeman.|Information om hur du aktiverar och konfigurerar energispar funktioner finns i [Konfigurera energispar funktioner](../../../../core/clients/manage/power/configuring-power-management.md).|  
|Rapporteringstjänstpunkt|Du måste konfigurera en Reporting Services-plats innan du kan visa rapporter för energisparfunktioner. Mer information finns i [Introduktion till rapportering](../../../servers/manage/introduction-to-reporting.md).|  
