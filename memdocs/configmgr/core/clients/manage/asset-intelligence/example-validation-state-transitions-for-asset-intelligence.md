---
title: Exempel på valideringstillståndsövergångar
titleSuffix: Configuration Manager
description: Se exempel på validerings tillstånds över gångar för Tillgångsinformation i Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6230a6e5-a1f6-459b-84f1-07fbde0e70f0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2af9243d6720d5821c641e5c80589457a33b638e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714180"
---
# <a name="example-validation-state-transitions-for-asset-intelligence"></a>Exempel på valideringstillståndsövergångar för Tillgångsinformation

*Gäller för: Configuration Manager (aktuell gren)*

Tillgångsinformation validerings tillstånd i Configuration Manager inte är statiska och kan ändras från administrativa åtgärder som du vidtar för att påverka de data som lagras i Tillgångsinformation katalogen. Det här avsnittet innehåller exempel på möjliga validerings tillstånds över gångar.

##  <a name="uncategorized-catalog-item-is-categorized-by-the-administrative-user"></a><a name="BKMK_UncategorizedIsCategorized"></a>Okategoriserade katalog objekt kategoriseras av den administrativa användaren  

|**Tillståndsövergång**|**Beskrivning av tillståndsövergång**|  
|--------------------------|--------------------------------------|  
|**Ej kategoriserade**|En inventerad programvarutitel som inte har kategoriserats förut av System Center Online eller som den administrativa användaren har lagt till i tillgångsinformationskatalogen.|  
|**Okategoriserade** till **UserDefined**|Det okategoriserade katalogobjektet kategoriseras av den administrativa användaren.|  

##  <a name="categorized-catalog-item-is-recategorized-by-the-administrative-user"></a><a name="BKMK_CategorizedIsReCategorized"></a> Kategoriserat katalogobjekt kategoriseras av den administrativa användaren.  

|**Tillståndsövergång**|**Beskrivning av tillståndsövergång**|  
|--------------------------|--------------------------------------|  
|**Verifierad**|Katalogobjekt har definierats av System Center Online-undersökare och finns i tillgångsinformationskatalogen.|  
|**Verifierad** till **Användardefinierad**|Det verifierade katalogobjektet kategoriseras om av den administrativa användaren.|  

> [!NOTE]  
>  Eftersom kategoriseringsinformationen som erhållits från System Center Online lagras i databasen och inte kan tas bort, kan den administrativa användaren återgå till System Center Online-kategoriseringen senare.  

##  <a name="user-defined-catalog-item-is-recategorized-by-system-center-online"></a><a name="BKMK_UserDefinedIsRecategorized"></a>Användardefinierat katalog objekt omkategoriseras av System Center Online  

|**Tillståndsövergång**|**Beskrivning av tillståndsövergång**|  
|--------------------------|--------------------------------------|  
|**Ej kategoriserade**|En inventerad programvarutitel som inte har kategoriserats förut av System Center Online eller av den administrativa användaren läggs till i tillgångsinformationskatalogen.|  
|**Användardefinierad**|Det okategoriserade katalogobjektet kategoriseras av den administrativa användaren.|  
|**Användardefinierad** till **Uppdaterbar**|Ett användardefinierat katalogobjekt har kategoriserats annorlunda av System Center Online vid efterföljande manuella massuppdateringar av tillgångsinformationskatalogen.<br /><br /> Den administrativa användaren kan använda dialogrutan **Konfliktlösning för programvaruinformation** och välja om den nya kategoriseringsinformationen eller det tidigare användardefinierade värdet ska användas.|  
|**Uppdaterbar** till **Verifierad**|Den administrativa användaren använder dialogrutan **Konfliktlösning för programvaruinformation** och väljer att använda den nya kategoriseringsinformationen som togs emot från System Center Online under den föregående kataloguppdateringen.|  
|eller||  
|**Uppdaterbar** till **Användardefinierad**|Den administrativa användaren använder dialogrutan **Konfliktlösning för programvaruinformation** och väljer att använda det tidigare användardefinierade värdet.|  

> [!NOTE]  
>  Eftersom kategoriseringsinformationen som erhållits från System Center Online lagras i databasen och inte kan tas bort, kan den administrativa användaren återgå till System Center Online-kategoriseringen senare.  

##  <a name="uncategorized-catalog-item-is-submitted-to-system-center-online-for-categorization"></a><a name="BKMK_UncategorizedIsSubmitted"></a>Okategoriserade-katalog objekt skickas till System Center Online för kategorisering  

|**Tillståndsövergång**|**Beskrivning av tillståndsövergång**|  
|--------------------------|--------------------------------------|  
|**Ej kategoriserade**|En inventerad programvarutitel som inte har kategoriserats förut av System Center Online eller av den administrativa användaren läggs till i tillgångsinformationsdatabasen.|  
|**Ej kategoriserade** till **Väntar**|Det okategoriserade objektet skickas till System Center Online för kategorisering av den administrativa användaren.|  
|**Väntar** till **Verifierad**|Objektet kategoriseras av System Center Online. Den administrativa användaren importerar objektet till tillgångsinformationskatalogen med hjälp av en masskataloguppdatering eller synkronisering av tillgångsinformationskatalogen. Båda är tillgängliga med platssystemrollen för en plats för synkronisering av tillgångsinformation.|  

##  <a name="user-defined-catalog-item-is-submitted-to-system-center-online-for-categorization"></a><a name="BKMK_UserDefinedIsSubmitted"></a>Användardefinierat katalog objekt skickas till System Center Online för kategorisering  

|**Tillståndsövergång**|**Beskrivning av tillståndsövergång**|  
|--------------------------|--------------------------------------|  
|**Ej kategoriserade**|En inventerad programvarutitel som inte har kategoriserats förut av System Center Online eller av en administrativ användare läggs till i tillgångsinformationsdatabasen.|  
|**Användardefinierad**|Du har kategoriserat det okategoriserade objektet.|  
|**Användardefinierad** till **Väntar**|Du kan skicka det användardefinierade objektet till System Center Online för kategorisering.|  
|**Väntar** till **Uppdaterbar**|Ett användardefinierat katalogobjekt har kategoriserats annorlunda av System Center Online under en efterföljande katalogsynkronisering. Du kan använda åtgärden **Lös konflikt** för att bestämma om du vill använda den nya kategoriseringsinformationen eller det tidigare användardefinierade värdet. Mer information om hur du löser konflikter finns i [Resolve software details conflicts](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails).|  
|**Uppdaterbar** till **Verifierad**|Du använder åtgärden **Lös konflikt** och väljer den nya kategoriseringsinformationen som togs emot av System Center Online under den föregående kataloguppdateringen. Mer information om hur du löser konflikter finns i [Resolve software details conflicts](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails).|  
|eller||  
|**Uppdaterbar** till **Användardefinierad**|Du använder åtgärden **Lös konflikt** och väljer att använda det tidigare användardefinierade värdet. Mer information om hur du löser konflikter finns i [Resolve software details conflicts](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails).|  

> [!NOTE]  
>  Eftersom kategoriseringsinformationen som erhållits från System Center Online lagras i databasen och inte kan tas bort, kan du återgå till System Center Online-kategoriseringen senare.  
