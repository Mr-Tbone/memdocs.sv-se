---
title: Använda Resursläsaren
titleSuffix: Configuration Manager
description: Använd Resursläsaren för att Visa maskin varu inventering i Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 375912f5-436d-4315-bdbe-d77afee6c9f3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: daa673169825638474fea05156fd837acbf0ba98
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710680"
---
# <a name="how-to-use-resource-explorer-to-view-hardware-inventory-in-configuration-manager"></a>Använda Resursläsaren för att Visa maskin varu inventering i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Använd Resursläsaren i Configuration Manager om du vill visa information om maskin varu inventering. Platsen samlar in den här informationen från klienter i hierarkin.  

> [!Tip]  
>  Resursläsaren visar inga data förrän en maskin varu inventerings cykel körs på klienten som du ansluter till.  



## <a name="overview"></a>Översikt

Resursläsaren innehåller följande avsnitt relaterade till maskin varu inventering:  

- **Maskin vara**: visar den senaste maskin varu inventering som samlats in från den angivna klient enheten.  

    - Noden **arbets Stations status** visar tiden och datumet för den senaste maskin varu inventeringen från enheten.  

- **Maskin varu historik**: en historik över inventerade objekt som har ändrats sedan den senaste maskin varu inventerings cykeln.  

    - Expandera ett objekt om du vill visa en **aktuell** nod och en eller flera noder med det historiska datumet. Jämför informationen i den aktuella noden med en av de historiska noderna för att se de objekt som har ändrats.  

> [!NOTE]  
> Som standard tar Configuration Manager bort maskin varu inventerings data som har varit inaktiva i 90 dagar. Justera antalet dagar i underhålls uppgiften **ta bort föråldrad lager historik** plats. Mer information finns i [underhålls aktiviteter](../../../servers/manage/maintenance-tasks.md).  



## <a name="how-to-open-resource-explorer"></a><a name="bkmk_open"></a>Så här öppnar du Resursläsaren   

1.  I Configuration Manager-konsolen går du till arbets ytan **till gångar och efterlevnad** och väljer noden **enheter** . Du kan också välja en samling i noden **enhets samlingar** .  

2.  Välj en enhet. I menyfliksområdet på fliken **Start** och gruppen **enheter** klickar du på **Start**och väljer sedan **Resursläsaren**.   

> [!Tip]  
> I Resursläsaren högerklickar du på ett objekt i det högra resultat fönstret för ytterligare åtgärder. Klicka på **Egenskaper** för att visa objektet i ett annat format.  



## <a name="use-of-large-integer-values"></a><a name="bkmk_bigint"></a>Användning av stora heltals värden
<!--1357880-->
I Configuration Manager version 1802 och tidigare har maskin varu inventeringen en gräns för heltal som är större än 4 294 967 296 (2 ^ 32). Den här gränsen kan nås för attribut som hård disk storlekar i byte. Hanterings platsen bearbetar inte heltals värden över den här gränsen, så inget värde lagras i databasen. 

Från och med version 1806 ökas gränsen till 18446744073709551616 (2 ^ 64). 

För en egenskap med ett värde som inte ändras, t. ex. total disk storlek, kan du inte omedelbart se värdet när du har uppgraderat platsen. De flesta maskin varu inventeringar är en delta rapport. Klienten skickar endast värden som ändras. Undvik det här problemet genom att lägga till en annan egenskap i samma klass. Den här åtgärden gör att klienten uppdaterar alla egenskaper i klassen som har ändrats. 



## <a name="see-also"></a>Se även

Information om hur du visar maskin varu inventering från klienter som kör Linux och UNIX finns i [övervaka klienter för Linux-och UNIX-servrar](../monitor-clients-for-linux-and-unix-servers.md).  

Resursläsaren visar också program varu inventering. Mer information finns i [använda Resursläsaren för att visa program varu inventering](use-resource-explorer-to-view-software-inventory.md).
