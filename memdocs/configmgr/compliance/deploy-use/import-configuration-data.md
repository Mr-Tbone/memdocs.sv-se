---
title: Importera konfigurationsdata
titleSuffix: Configuration Manager
description: Importera konfigurations data om de finns i ett CAB-filformat och följer schemat för service Modeling-språket som stöds.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 309b9a09-a611-4ba2-90ab-dde51582cf87
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 4f70a956051858fce5b4ba5f519c7e1035600793
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712311"
---
# <a name="import-configuration-data-with-configuration-manager"></a>Importera konfigurations data med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Förutom att skapa konfigurations bas linjer och konfigurations objekt i Configuration Manager-konsolen kan du importera konfigurations data om de finns i ett CAB-filformat (CAB) och följer det som stöds av SML-schemat (service Modeling Language). Du kan importera konfigurations data från:  

- Rekommenderade konfigurationsdata (konfigurationspaket) som har hämtats från Microsoft eller andra programleverantörer.  

- Konfigurations data som har exporter ATS från System Center 2012 Configuration Manager och senare.  

- Konfigurations data som har skapats externt och som följer SML-schemat.  

  Ett exempel på ett konfigurationspaket som hjälper dig att hantera kompatibiliteten för platsserverroller i System Center 2012 Configuration Manager finns i [System Center 2012 Configuration Manager Configuration Pack](https://www.microsoft.com/download/details.aspx?id=30710&WT.mc_id=rss_alldownloads_all).  

När du importerar en konfigurationsbaslinje kan vissa eller alla konfigurationsobjekt som konfigurationsbaslinjen refererar till även ingå i kabinettfilen. Under importen verifierar Configuration Manager att alla konfigurations objekt som refereras i konfigurations bas linjen också ingår i CAB-filen eller redan finns på den Configuration Manager webbplatsen. Import processen Miss lyckas om du försöker importera en konfigurations bas linje som refererar till konfigurations data som Configuration Manager inte kan hitta.  

Exempel på andra scenarier där importen kan misslyckas är:  

-   Konfigurations data refererar till konfigurations data som Configuration Manager inte kan hitta, antingen i sin databas eller i själva CAB-filen.  

-   Konfigurations data finns redan i Configuration Manager databasen med samma namn och konfigurations data version, men innehålls versionen skiljer sig åt.  

-   Konfigurations data finns redan i Configuration Manager-databasen med samma innehålls version, men hash-beräkningen identifierar den som en annan.  

-   En nyare version av konfigurations data med samma namn finns redan eller har nyligen tagits bort i Configuration Manager databasen.  

-   I en Configuration Manager hierarki med flera platser importerades konfigurations data ursprungligen från en överordnad plats. Du måste uppdatera dem från samma plats och inte en underordnad plats.  

### <a name="import-configuration-data"></a>Importera konfigurationsdata  

1.  I Configuration Manager-konsolen klickar du på **till gångar och efterlevnad** > **konfigurations objekt** eller **konfigurations bas linjer**
2.  På fliken **Start** går du till gruppen **skapa** och klickar på **Importera konfigurations data**.  
3.  Klicka på **Lägg till** på sidan **Markera filer**i guiden **Importera konfigurationsdata**och välj de CAB-filer som du vill importera i dialogrutan **Öppna** .  
4.  Markera kryss rutan **skapa en ny kopia av de importerade konfigurations bas linjerna och konfigurations objekt** om du vill att importerade konfigurations data ska kunna redige ras i Configuration Manager-konsolen.  
5.  På sidan **Sammanfattning** granskar du de åtgärder som ska vidtas och slutför sedan guiden.  

Importerade konfigurations data visas i noden **kompatibilitetsinställningar** i arbets ytan **till gångar och efterlevnad** .  
