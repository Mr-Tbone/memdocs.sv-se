---
title: Skapa underordnade konfigurationsobjekt
titleSuffix: Configuration Manager
description: Skapa underordnade konfigurations objekt i Configuration Manager.
ms.date: 05/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 113984fa-6150-41a1-89ed-d2a83b979732
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 319f673200244d4451b957dcb778ce378f9569fa
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240328"
---
# <a name="how-to-create-child-configuration-items-in-configuration-manager"></a>Så här skapar du underordnade konfigurations objekt i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Underordnade konfigurations objekt i Configuration Manager är kopior av konfigurations objekt som behåller en relation till det ursprungliga konfigurationsobjektet där de ärver den ursprungliga konfigurationen från det överordnade konfigurationsobjektet.  

När du visar egenskaperna för ett underordnat konfigurations objekt i Configuration Manager-konsolen kan du inte redigera ärvda objekt och inställningar med deras validerings villkor. Men du kan lägga till och redigera ytterligare valideringskriterier till det underordnade konfigurationsobjektet och du kan också lägga till nya objekt och inställningar till det underordnade konfigurationsobjektet.
Ett exempel på att skapa och redigera ett underordnat konfigurations objekt är att förfina det ursprungliga konfigurationsobjektet så att det passar dina affärs behov.  

> [!NOTE]  
>  Du kan bara skapa underordnade konfigurationsobjekt från konfigurationsobjekt av typen **Windows-baserade datorer och servrar (anpassat)**.  

## <a name="to-create-a-child-configuration-item"></a>Så här skapar du ett underordnat konfigurationsobjekt  

1.  I Configuration Manager-konsolen klickar du på **till gångar och**kompatibilitetsinställningar  >  **kompatibilitetsinställningar**  >  **konfigurations objekt**.  

3.  Välj det konfigurationsobjekt som du vill skapa ett underordnat konfigurationsobjekt för i listan **Konfigurationsobjekt** och klicka på **Skapa underordnat konfigurationsobjekt** i gruppen **Konfigurationsobjekt** på fliken **Start**.  

4.  På sidan **Allmänt** i guiden **Skapa underordnat konfigurationsobjekt**kan du välja en specifik version av det överordnade konfigurationsobjektet för att skapa det underordnade objektet. Andra steg i den här guiden är identiska med de som du använder för att skapa ett standardkonfigurationsobjekt. Mer information finns i [så här skapar du anpassade konfigurations objekt för Windows-datorer och serverdatorer](../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md).  

5.  Slutför guiden. Det nya underordnade konfigurationsobjektet visas i listan **Konfigurationsobjekt** .  
