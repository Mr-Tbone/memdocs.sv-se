---
title: Hantera konfigurationsdata
titleSuffix: Configuration Manager
description: När du har skapat konfigurations objekt och bas linjer i Configuration Manager kan du använda andra kommandon för att utföra olika åtgärder.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: b48c693c-d2b0-4707-a5dd-fe92172c49fe
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: c375b5d773775e1be89f1e9dda38ee04e7f9f63f
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240260"
---
# <a name="manage-configuration-data-in-configuration-manager"></a>Hantera konfigurations data i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

När du har skapat konfigurations objekt och konfigurations bas linjer i Configuration Manager finns ytterligare kommandon som hjälper dig att utföra olika åtgärder.  

## <a name="manage-configuration-items"></a>Hantera konfigurations objekt  

-   I arbets ytan **till gångar och efterlevnad** **expanderar du kompatibilitetsinställningar**  >  **konfigurations objekt**, väljer det konfigurations objekt som ska hanteras och väljer sedan en hanterings aktivitet.  

|Hanteringsaktivitet|Information|  
|---------------------|-------------|  
|**Skapa underordnat konfigurationsobjekt**|Öppnar **Skapa underordnat konfigurationsobjekt** där du kan skapa ett underordnat konfigurationsobjekt från det valda konfigurationsobjektet.<br /><br /> Du kan inte skapa ett underordnat konfigurationsobjekt från ett konfigurationsobjekt för mobil enhet.<br /><br /> Mer information finns i [skapa underordnade konfigurations objekt](../../compliance/deploy-use/create-child-configuration-items.md).|  
|**Revisionshistorik**|Öppnar dialogrutan **Revisionshistorik för konfigurationsobjekt** där du kan visa och hantera tidigare revisioner av det valda konfigurationsobjektet.|  
|**Visa XML-definition**|XML-definitionsfilen för det valda konfigurationsobjektet visas i ett nytt fönster. Den här informationen kan vara användbar om du vill redigera konfigurationsdata manuellt.|  
|**Export**|Exporterar ett konfigurationsobjekt i arkivfilformat (CAB), om det skapades på den platsen. Du kan sedan importera den till samma eller en annan Configuration Manager webbplats. Konfigurationsdata omvandlas till DCM-samling.|  
|**Kopiera**|Skapar en kopia av det valda konfigurationsobjektet med ett namn som du anger. Det nya konfigurationsobjektet behåller ingen relation till det ursprungliga konfigurationsobjektet. Det innebär att det kopierade konfigurationsobjektet inte fortsätter att ärva konfigurationsinformation från det ursprungliga objektet.|  
|**Ta bort**|Öppnar dialogrutan **Ta bort konfigurationsobjekt** där alla referenser till konfigurationsobjektet visas.<br /><br /> Du måste ta bort alla referenser till ett konfigurationsobjekt innan du kan ta bort själva objektet.|  

## <a name="manage-configuration-baselines"></a>Hantera konfigurations bas linjer  

-   I arbets ytan **till gångar och efterlevnad** **expanderar du kompatibilitetsinställningar**  >  **konfigurations bas linjer**, väljer den konfigurations bas linje som ska hanteras och väljer sedan en hanterings aktivitet.  


|Hanteringsaktivitet|Information|  
|---------------------|-------------|  
|**Visa medlemmar**|Visar alla konfigurationsobjekt som konfigurationsbaslinjen hänvisar till.|  
|**Schemalägg sammanfattning**|Konfigurerar det schema enligt vilket data som visas i noden **konfigurations bas linjer** i Configuration Manager-konsolen uppdateras med den senaste informationen från plats databasen.|  
|**Kör sammanfattning**|Med sammanfattning uppdateras informationen i noden **Konfigurationsbaslinjer** med den senaste informationen från platsdatabasen. Det kan ta flera minuter att slutföra åtgärden. Du kan behöva klicka på **Uppdatera** innan de senaste data visas i konsolen.|  
|**Visa XML-definition**|XML-definitionsfilen för den valda konfigurationsbaslinjen visas i ett nytt fönster. Den här informationen kan vara användbar om du vill redigera konfigurationsdata manuellt.|  
|**Aktivera**|Aktiverar en konfigurationsbaslinje för övervakning av kompatibiliteten.|  
|**Inaktivera**|Inaktiverar en konfigurationsbaslinje för att inte längre utvärdera kompatibiliteten på klientdatorer. Även de konfigurationsbaslinjer som hänvisar till den här baslinjen inaktiveras.|  
|**Export**|Exporterar en konfigurationsbaslinje i arkivfilformat (CAB), om den skapades på den platsen. Du kan sedan importera den till samma eller en annan Configuration Manager webbplats. Konfigurationsdata omvandlas till DCM-samling.<br /><br /> Information om hur du importerar konfigurations data finns i [Importera konfigurations data](../../compliance/deploy-use/import-configuration-data.md).|  
|**Kopiera**|Skapar en kopia av den valda konfigurationsbaslinjen med ett namn som du anger. Den nya konfigurationsbaslinjen behåller ingen relation till den ursprungliga konfigurationsbaslinjen.|  
|**Ta bort**|Öppnar dialogrutan **Ta bort konfigurationsbaslinje** där alla referenser till konfigurationsbaslinjen visas.<br /><br /> Du måste ta bort alla referenser till en konfigurationsbaslinje innan du kan ta bort själva baslinjen.|  
|**Distribuera**|Öppnar dialogrutan **Distribuera konfigurationsbaslinje** där du kan distribuera en eller flera konfigurationsbaslinjer till enheter i hierarkin.<br /><br /> Mer information finns i [distribuera konfigurations bas linjer](../../compliance/deploy-use/deploy-configuration-baselines.md).|  
