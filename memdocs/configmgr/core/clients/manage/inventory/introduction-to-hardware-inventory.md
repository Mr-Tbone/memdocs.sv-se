---
title: 'Maskinvaruinventering '
titleSuffix: Configuration Manager
description: Få en introduktion till maskin varu inventering i Configuration Manager.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3969952e-9d05-49c9-82a2-e7e90ccef511
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7baf6bad80fbccb698278602c519f3a75b8a4b5f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714411"
---
# <a name="introduction-to-hardware-inventory-in-configuration-manager"></a>Introduktion till maskin varu inventering i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Använd maskin varu inventering i Configuration Manager om du vill samla in information om maskin varu konfigurationen för klient enheter i din organisation. Om du vill samla in maskin varu inventering måste du välja inställningen **Aktivera maskin varu inventering på klienter** i klient inställningar.  

 När maskin varu inventering har Aktiver ATS och klienten kör en maskin varu inventerings cykel skickar klienten informationen till en hanterings plats på klientens plats. Hanterings platsen vidarebefordrar sedan inventerings informationen till Configuration Manager plats servern, som lagrar inventerings informationen i plats databasen. Maskinvaruinventeringen körs på klienter enligt det schema som du anger i klientinställningarna.  
## <a name="view-hardware-inventory"></a>Visa maskin varu inventering 

 Du kan använda flera metoder för att Visa maskin varu inventerings data som Configuration Manager samlar in, inklusive följande metoder:  

- [Skapa frågor som returnerar enheter som baseras på en speciell maskin varu konfiguration](../../../../core/servers/manage/introduction-to-queries.md).  

- [Skapa frågebaserade samlingar som baseras på en speciell maskin varu konfiguration](../../../../core/clients/manage/collections/introduction-to-collections.md). Frågebaserade samlingsmedlemskap uppdateras automatiskt enligt ett schema. Du kan använda samlingar för flera uppgifter, inklusive program varu distribution.

- [Kör rapporter som visar detaljerad information om maskinvarukonfigurationer i din organisation](../../../servers/manage/introduction-to-reporting.md).

- [Använd Resursläsaren](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) om du vill visa detaljerad information om maskin varu inventeringen som samlas in från klient enheter.

När maskinvaruinventering körs på en klientenhet är de första inventeringsdata som klienten returnerar alltid en fullständig inventering. Efterföljande inventerings data innehåller bara förändrings inventerings information. Plats servern bearbetar förändrings inventerings information i den ordning som tas emot. Om delta information för en klient saknas, avvisar plats servern ytterligare delta information och dirigerar klienten för att köra en fullständig inventerings cykel.  

 Configuration Manager ger begränsat stöd för datorer med flervalsstart. Configuration Manager kan identifiera datorer med flervalsstart men returnerar bara inventerings information från det operativ system som är aktivt när inventerings cykeln körs.  

> [!NOTE]  
>  Information om hur du använder maskin varu inventering med klienter som kör Linux och UNIX finns i [maskin varu inventering för Linux och UNIX](../../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md).  

## <a name="extending-configuration-manager-hardware-inventory"></a>Utöka maskinvaruinventeringen för Configuration Manager  
 Förutom den inbyggda maskin varu inventeringen i Configuration Manager kan du också använda någon av dessa metoder för att utöka maskin varu inventeringen för att samla in mer information:  

- Aktivera, inaktivera, lägga till och ta bort inventerings klasser för maskin varu inventering från Configuration Manager-konsolen.  
- Använd NOIDMIF-filer för att samla in information om klient enheter som inte kan inventeras av Configuration Manager. Du kanske till exempel vill samla in information om enheternas tillgångsnummer som endast förekommer som en etikett på enheten. NOIDMIF-inventeringen associeras automatiskt med klientenheten som den samlats in från.  
- Använd IDMIF-filer för att samla in information om till gångar som inte är associerade med en Configuration Manager-klient, till exempel projektorer, Foto kopiatorer och nätverks skrivare.


## <a name="next-steps"></a>Nästa steg
Mer information om hur du använder dessa metoder för att utöka Configuration Manager maskin varu inventering finns i [så här konfigurerar du maskin varu inventering](../../../../core/clients/manage/inventory/configure-hardware-inventory.md).  
