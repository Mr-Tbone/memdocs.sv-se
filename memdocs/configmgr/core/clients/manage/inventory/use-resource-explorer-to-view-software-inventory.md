---
title: Visa program varu inventering med Resursläsaren
titleSuffix: Configuration Manager
description: Använd Resursläsaren för att visa program varu inventering i Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4b7aa5f6-5ebd-49be-b7f3-4206caadc187
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 08905a72b6af6e9eae4d2cef9f4732ef692dc134
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710659"
---
# <a name="how-to-use-resource-explorer-to-view-software-inventory-in-configuration-manager"></a>Använda Resursläsaren för att visa program varu inventering i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Använd Resursläsaren i Configuration Manager för att visa information om program varu inventering som har samlats in från datorer i hierarkin.  

> [!NOTE]  
>  Resursläsaren visar inga inventerings data förrän en program varu inventerings cykel har körts på klienten.  

 Resursläsaren innehåller följande information om program varu inventering:  

-   **Program vara**:  

    -   **Insamlade filer** – filer som samlats in under program varu inventeringen.  

    -   **Fil information** – filer som har inventerats under program varu inventeringen och som inte är associerade med en speciell produkt eller tillverkare.  

    -   **Senaste program varu genomsökning** – datum och tid för den senaste program varu inventeringen och fil insamlingen för klient datorn.  

    -   **Produkt information** – program varu produkter som inventerats av program varu inventeringen, grupperade efter tillverkare.  

## <a name="to-run-resource-explorer-from-the-configuration-manager-console"></a>Så här kör du Resursläsaren från Configuration Manager-konsolen  

1.  I Configuration Manager-konsolen väljer du **till gångar och efterlevnad**

2.  Välj **enheter** på arbets ytan **till gångar och efterlevnad** eller öppna en samling som visar enheter.  

3.  Välj den dator som innehåller den inventering som du vill visa och välj sedan **Starta** > **Resursläsaren**på fliken **Start** > **enheter** .

4.  Du kan högerklicka på ett objekt i den högra rutan i fönstret Resursläsaren och välja **Egenskaper** för att visa den insamlade inventerings informationen i ett mer läsbart format.  
 
## <a name="view-and-manage-collected-diagnostic-files"></a><a name="bkmk_diag"> </a> Visa och hantera insamlade diagnostikfiler

Från och med Configuration Manager version 2002 använder du Resursläsaren för att visa och hantera de filer som samlats in när du använder klient meddelanden för att [samla in klient loggar](../client-notification.md#client-diagnostics). 

1. Från noden **enheter** högerklickar du på den enhet som du vill visa loggarna för.
1. Välj **Start**och sedan **Resursläsaren**.
1. Klicka på **diagnostiska filer**från **Resursläsaren**.
1. I listan **diagnostikfiler** kan du se samlings datumet för filerna. Namn formatet för klient loggarna är `Support_<guid>.zip`.
1. Högerklicka på zip-filen och välj ett av följande alternativ:
    - **Öppna Support Center**: startar [Support Center](../../../support/support-center.md).
    - **Kopiera**: rad informationen kopieras från Resursläsaren.
    - **Visa fil**: öppnar mappen där zip-filen finns i Utforskaren.
    - **Spara**: öppnar dialog rutan Spara fil för den valda filen.
    - **Exportera**: sparar de Resursläsaren kolumner som visas i **diagnostikfiler**.
    - **Uppdatera**: uppdaterar fil listan.
    - **Egenskaper**: returnerar egenskaperna för den valda filen. 

[![Granska och spara klient loggar från Resursläsaren](./../media/4226618-view-collected-client-logs.png)](./../media/4226618-view-collected-client-logs.png#lightbox)

## <a name="next-steps"></a>Nästa steg

[Använd Support Center](../../../support/support-center.md) för att Visa insamlade diagnostikfiler.
