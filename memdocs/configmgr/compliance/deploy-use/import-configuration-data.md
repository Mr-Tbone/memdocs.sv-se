---
title: Importera konfigurationsdata
titleSuffix: Configuration Manager
description: Importera konfigurations data om de finns i ett CAB-filformat och följer schemat för service Modeling-språket som stöds.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 309b9a09-a611-4ba2-90ab-dde51582cf87
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 7d9760a49815b9eb33c7886f4d9a8f9637dedd21
ms.sourcegitcommit: 9f072da27aa64f46a9409470b5dac5bfac3a0fe5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/04/2020
ms.locfileid: "89468319"
---
# <a name="import-configuration-data-with-configuration-manager"></a>Importera konfigurations data med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Förutom att skapa konfigurations bas linjer och konfigurations objekt i Configuration Manager-konsolen kan du importera konfigurations data om de finns i ett CAB-filformat (CAB) och följer det som stöds av SML-schemat (service Modeling Language). Du kan importera konfigurations data från:  

- Rekommenderade konfigurationsdata (konfigurationspaket) som har hämtats från Microsoft eller andra programleverantörer.  

- Konfigurations data som har exporter ATS från System Center 2012 Configuration Manager och senare.  

- Konfigurations data som har skapats externt och som följer SML-schemat.  

När du importerar en konfigurationsbaslinje kan vissa eller alla konfigurationsobjekt som konfigurationsbaslinjen refererar till även ingå i kabinettfilen. Under importen verifierar Configuration Manager att alla konfigurations objekt som refereras i konfigurations bas linjen också ingår i CAB-filen eller redan finns på den Configuration Manager webbplatsen. Import processen Miss lyckas om du försöker importera en konfigurations bas linje som refererar till konfigurations data som Configuration Manager inte kan hitta.  

Exempel på andra scenarier där importen kan misslyckas är:  

-   Konfigurations data refererar till konfigurations data som Configuration Manager inte kan hitta, antingen i sin databas eller i själva CAB-filen.  

-   Konfigurations data finns redan i Configuration Manager databasen med samma namn och konfigurations data version, men innehålls versionen skiljer sig åt.  

-   Konfigurations data finns redan i Configuration Manager-databasen med samma innehålls version, men hash-beräkningen identifierar den som en annan.  

-   En nyare version av konfigurations data med samma namn finns redan eller har nyligen tagits bort i Configuration Manager databasen.  

-   I en Configuration Manager hierarki med flera platser importerades konfigurations data ursprungligen från en överordnad plats. Du måste uppdatera dem från samma plats och inte en underordnad plats.  

### <a name="import-configuration-data"></a>Importera konfigurationsdata  

1.  I Configuration Manager-konsolen klickar du på **till gångar och efterlevnad**  >  **konfigurations objekt** eller **konfigurations bas linjer**
2.  På fliken **Start** går du till gruppen **skapa** och klickar på **Importera konfigurations data**.  
3.  Klicka på **Lägg till** på sidan **Markera filer**i guiden **Importera konfigurationsdata**och välj de CAB-filer som du vill importera i dialogrutan **Öppna** .  
4.  Markera kryss rutan **skapa en ny kopia av de importerade konfigurations bas linjerna och konfigurations objekt** om du vill att importerade konfigurations data ska kunna redige ras i Configuration Manager-konsolen.  
5.  På sidan **Sammanfattning** granskar du de åtgärder som ska vidtas och slutför sedan guiden.  

Importerade konfigurations data visas i noden **kompatibilitetsinställningar** i arbets ytan **till gångar och efterlevnad** .  
