---
title: Programvaruinventering
titleSuffix: Configuration Manager
description: Få en introduktion till program varu inventering i Configuration Manager.
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 79eb49da-cd2b-4ffc-b355-b595aeba3aea
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 07b6f0108125c97128ddc88b663b0af4dabadbe7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714397"
---
# <a name="introduction-to-software-inventory-in-configuration-manager"></a>Introduktion till program varu inventering i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Använd program varu inventering för att samla in information om filer på klient enheter. Program varu inventering kan också samla in filer från klient enheter och lagra dem på plats servern. Program varu inventering samlas in när du väljer inställningen **Aktivera program varu inventering på klienter** i klient inställningar. Du kan också schemalägga åtgärden i klient inställningar.  

När du har aktiverat program varu inventering och klienterna kör en program varu inventerings cykel skickar klienten informationen till en hanterings plats på klientens plats. Hanterings platsen vidarebefordrar sedan inventerings informationen till Configuration Manager plats servern, där informationen lagras i plats databasen.

 Det finns några sätt att visa program varu inventerings data:  

- [Skapa frågor](../../../../core/servers/manage/create-queries.md) som returnerar enheter med angivna filer.   

- Skapa [frågebaserade samlingar](../../../../core/clients/manage/collections/introduction-to-collections.md) som innehåller enheter med angivna filer.   

- [Kör rapporter](../../../servers/manage/introduction-to-reporting.md) som innehåller information om filer på enheter.

- Använd [Resursläsaren](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md) för att granska detaljerad information om de filer som har inventerats och samlats in från klient enheter.   

 När program varu inventeringen körs på en klienten het är den första rapporten en fullständig inventering. Efterföljande rapporter innehåller endast ändringar i inventerings information. Plats servern bearbetar delta informationen i den mottagna ordern. Om delta information för en klient saknas avvisar plats servern ytterligare delta information och dirigerar klienten för att köra en fullständig inventering.  

 Configuration Manager kan identifiera datorer med flervalsstart men returnerar bara inventerings information från det operativ system som är aktivt vid tidpunkten för inventeringen.  
