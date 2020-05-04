---
title: Förbered för hantering av programuppdateringar
titleSuffix: Configuration Manager
description: För att förbereda för att hantera uppdateringar slutför du dessa uppgifter för att Visa utvärderings data för kompatibilitet i Configuration Manager-konsolen.
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 01907900-e28b-4cd7-9479-42906416707b
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: ab22fdcacf7574884f7cfd21859cb4b1aeb8e23f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717274"
---
# <a name="prepare-for-software-updates-management"></a>Förbered för hantering av programuppdateringar

*Gäller för: Configuration Manager (aktuell gren)*

Innan utvärderings data för kompatibiliteten för program uppdateringen visas i Configuration Manager-konsolen och innan du kan distribuera program uppdateringar till klient datorer, måste du utföra stegen i följande avsnitt.

## <a name="step-1-install-a-software-update-point"></a>Steg 1: installera en program uppdaterings plats  
Program uppdaterings platsen krävs på den centrala administrations platsen, eller på en fristående primär plats, och på primära platser kan du aktivera utvärdering av kompatibilitet för program uppdateringar och distribuera program uppdateringar till klienter. Programuppdateringsplatsen på sekundära platser är valfri. Mer information finns i [installera en program uppdaterings plats](install-a-software-update-point.md)  

## <a name="step-2-synchronize-software-updates"></a>Steg 2: Synkronisera programuppdateringar
Synkronisering av program uppdateringar innebär att metadata för program uppdateringar hämtas som uppfyller de kriterier som du konfigurerar. Program uppdateringar visas inte i Configuration Manager-konsolen förrän du synkroniserar program uppdateringar. Mer information finns i [Synkronisera program uppdateringar](synchronize-software-updates.md).   

## <a name="step-3-configure-classifications-and-products-to-synchronize"></a>Steg 3: Konfigurera klassificeringar och produkter som ska synkroniseras
Gör den här konfigurationen på den centrala administrationsplatsen eller fristående primära platsen. När du synkroniserar program uppdateringar första gången hämtar Configuration Manager en uppdaterad lista över klassificeringar och produkter. Nu kan du välja bland de nya alternativen i egenskaperna för komponenten för program uppdaterings plats. När du har konfigurerat nya klassificeringar och produkter upprepar du steg 2 för att starta synkroniseringen av program uppdateringar för att hämta metadata för program uppdateringar för de nya kriterierna. Mer information finns i [Konfigurera klassificeringar och produkter som ska synkroniseras](configure-classifications-and-products.md).

## <a name="step-4-manage-settings-for-software-updates"></a>Steg 4: hantera inställningar för program uppdateringar
När du har synkroniserat program uppdateringar kontrollerar du Configuration Manager klient inställningar, grup princip konfiguration och inställningar för program uppdateringar innan du distribuerar program uppdateringar. Mer information finns i [Hantera inställningar för program uppdateringar](manage-settings-for-software-updates.md).
