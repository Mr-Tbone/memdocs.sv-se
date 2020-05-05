---
title: Funktioner i Technical Preview 1608
titleSuffix: Configuration Manager
description: Lär dig mer om funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1608.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 63e1df5e-637c-4b07-b7ec-95340f43a805
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: fd668760a6b5d1a16cfbb8549063da4f7e8a8b7d
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074188"
---
# <a name="capabilities-in-technical-preview-1608-for-configuration-manager"></a>Funktioner i Technical Preview 1608 för Configuration Manager

*Gäller för: Configuration Manager (Technical Preview Branch)*

Den här artikeln beskriver de funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1608. Du kan installera den här versionen för att uppdatera och lägga till nya funktioner till din Configuration Manager Technical Preview-webbplats.      Innan du installerar den här versionen av Technical Preview kan du läsa introduktions avsnittet, [teknisk för hands version för Configuration Manager](../../core/get-started/technical-preview.md), för att bekanta dig med allmänna krav och begränsningar för att använda en teknisk för hands version, hur du uppdaterar mellan versioner och hur du ger feedback om funktionerna i en teknisk för hands version.    


**Följande är nya funktioner som du kan prova med den här versionen.**  




##  <a name="improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step"></a>Förbättringar av aktivitetssekvenssteget Förbered ConfigMgr-klienten för avbildning  
Steget Förbered ConfigMgr-klient tar nu bort Configuration Manager-klienten fullständigt, i stället för att bara ta bort viktig information. När aktivitetssekvensen distribuerar den avbildade operativ Systems avbildningen kommer den att installera en ny Configuration Manager-klient varje gång.  


## <a name="improvements-to-software-center"></a>Förbättringar av Software Center
* På flikarna Software Center- **program**, **uppdateringar**och **operativ system** visas nu vilken program vara som nyligen har lagts till. Siffror i navigerings fönstret visar hur många nya program varor som finns på varje flik.
* Användarna kan nu begära godkännande för program och sedan Visa begär ande historiken i vyn **programinformation** i Software Center. Knappen **begär** i **program information** omdirigeras inte längre till den webbaserade programkatalog.

## <a name="improvements-to-asset-intelligence"></a>Förbättringar av Tillgångsinformation
Vi har lagt till ett fält i egenskaperna för Inventerad program vara som gör att du kan ange en överordnad och underordnad relation med annan program vara. I listan Inventerad program vara kan du Visa överordnad program vara och även dölja all underordnad program vara.

### <a name="configure-a-parent-to-child-relationship"></a>Konfigurera en överordnad till underordnad relation
  1. Om du vill ange överordnad program vara går du till noden Inventerad program vara, högerklickar på ett program varu objekt i listan **Inventerad program vara** och väljer **Egenskaper**.
  2. I dialog rutan som öppnas väljer du den program vara som du vill ange som överordnad program vara för det första valet.

### <a name="filter-the-software-display"></a>Filtrera program varu visningen
När du har definierat överordnade till underordnade relationer kan du filtrera vyn så att den endast visar program vara som är överordnad eller som inte har någon definierad relation. Detta döljer all program vara som har angetts som underordnad en annan Inventerad program vara. Gör så här:
   1. I Sök fältet väljer du att **lägga till villkor**
   2. Välj **överordnad program vara** och ändra villkor svärdet till **är tomt**och klicka sedan på **Sök**.

På skärmen visas nu bara de överordnade program varu objekt eller program vara som inte har några definierade relationer. Program vara som endast är underordnad en annan rubrik visas inte.

## <a name="remote-control-keyboard-translation"></a>Översättning av fjärr styrnings tangent bord
Tidigare har Configuration Manager överfört nyckel positionen från visnings platsen till delnings platsen. Detta var problematisk för tangent bords konfigurationer som skiljer sig från visnings programmet till delare. Ett visnings program med ett engelskt tangent bord skulle t. ex. skriva "A", men delarnas franska tangent bord skulle ge en "Q". Vi ändrar standard beteendet så att själva själva figuren skickas från Viewers tangent bord till delningen, och vad visnings programmet avser att skriva kommer till delningen.

Detta kan inaktive ras av visnings programmet om de föredrar att skriva enligt delarnas tangent bords ordning. Om du vill ändra beteendet väljer du **åtgärd**i **Configuration Manager fjärr styrning**och väljer **Aktivera tangent bords översättning** för att överföra nyckel position.

> [!NOTE]
>
> Särskilda nycklar, till exempel ~! # @ $%, kommer inte att översättas korrekt.
