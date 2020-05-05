---
title: 'Lägga till uppdateringar i en uppdaterings grupp '
titleSuffix: Configuration Manager
description: Manuellt eller Lägg automatiskt till program uppdateringar i en program uppdaterings grupp i din miljö.
ms.date: 03/18/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: a0767664-fd60-46a8-9da5-86cc431ce53c
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: c38ed629e606d3f891a6473866d0e8eda40eade1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723910"
---
# <a name="add-software-updates-to-an-update-group"></a>Lägga till programuppdateringar i en uppdateringsgrupp  

*Gäller för: Configuration Manager (aktuell gren)*

 Med programuppdateringsgrupper får du ett effektivt sätt att organisera programuppdateringar i din miljö. Du kan lägga till programuppdateringar i en programuppdateringsgrupp manuellt eller lägga till dem i en programuppdateringsgrupp automatiskt med hjälp av en automatisk distributionsregel. Du kan även distribuera en programuppdateringsgrupp manuellt eller distribuera gruppen automatiskt med hjälp av en automatisk distributionsregel. När du har distribuerat en program uppdaterings grupp kan du lägga till nya program uppdateringar i gruppen och Configuration Manager distribuera dem automatiskt. Använd följande procedurer om du vill lägga till programuppdateringar i en ny eller befintlig programuppdateringsgrupp.  

#### <a name="to-add-software-updates-to-a-new-software-update-group"></a>Lägga till programuppdateringar i en ny programuppdateringsgrupp  

1.  I Configuration Manage-konsolen klickar du på **Programbibliotek**.  

2.  Expandera **Programuppdateringar** i arbetsytan Programvarubibliotek och klicka sedan på **Alla programuppdateringar**.  

3.  Välj de programuppdateringar som ska läggas till i den nya programuppdateringsgruppen.  

4.  Klicka på **Skapa programuppdateringsgrupp** i gruppen **Uppdatera** på fliken **Start**.  

5.  Ange ett namn på programuppdateringsgruppen och tillhandahåll eventuellt en beskrivning. Använd ett namn och en beskrivning som ger tillräckligt med information för att du ska kunna avgöra vilken typ av programuppdateringar som finns i programuppdateringsgruppen. Klicka på **Skapa**om du vill fortsätta.  

6.  Klicka på **Programuppdateringsgrupper** om du vill visa den nya programuppdateringsgruppen.  

7.  Välj programuppdateringsgruppen och klicka på **Visa medlemmar** i gruppen **Uppdatera** på fliken **Start** . Nu visas en lista över de programuppdateringar som finns med i gruppen.  

#### <a name="to-add-software-updates-to-an-existing-software-update-group"></a>Lägga till programuppdateringar till en befintlig programuppdateringsgrupp  

1.  I Configuration Manage-konsolen klickar du på **Programbibliotek**.  

2.  Expandera **Programuppdateringar** i arbetsytan Programvarubibliotek och klicka sedan på **Alla programuppdateringar**.  

3.  Välj de programuppdateringar som du vill lägga till i den nya programuppdateringsgruppen.  

    > [!NOTE]  
    >  I noden **alla program uppdateringar** visar Configuration Manager alla uppdateringar förutom de i klassificeringen **uppgraderingar** och **Office 365-klient** produkt.  

4.  Klicka på **Redigera medlemskap** på fliken **Start** i gruppen **Uppdatera**.  

5.  Välj den programuppdateringsgrupp där du vill lägga till programuppdateringarna.  

6.  Klicka på noden **Programuppdateringsgrupper** för att visa programuppdateringsgruppen.  

7.  Välj programuppdateringsgruppen och klicka på **Visa medlemmar** i gruppen **Uppdatera** på fliken **Start** så visas en lista över de programuppdateringar som ingår i programuppdateringsgruppen.  
