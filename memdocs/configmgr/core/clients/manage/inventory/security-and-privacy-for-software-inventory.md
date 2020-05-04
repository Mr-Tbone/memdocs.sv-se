---
title: Säkerhets sekretess för program varu inventering
titleSuffix: Configuration Manager
description: Hämta information om säkerhet och sekretess för program varu inventering i Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 8e68e1fb-a8ec-4543-bb8a-cbbaf184a418
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d64fd2ac98996a6a1ccadae78e5f9cc576b55444
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710673"
---
# <a name="security-and-privacy-for-software-inventory-in-configuration-manager"></a>Säkerhet och sekretess för program varu inventering i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Det här avsnittet innehåller information om säkerhet och sekretess för program varu inventering i Configuration Manager.  

##  <a name="security-best-practices-for-software-inventory"></a><a name="BKMK_Security_HardwareInventory"></a> Rekommenderade säkerhetsmetoder för programvaruinventering  
 Använd följande rekommenderade säkerhetsmetoder när du samlar in inventeringsdata från klienter:  

|Regelverk för säkerhet|Mer information|  
|----------------------------|----------------------|  
|Signera och kryptera inventeringsdata|När klienterna kommunicerar med hanteringsplatser med hjälp av HTTPS krypteras alla data som de skickar med hjälp av SSL. Men när klientdatorer använder HTTP för att kommunicera med hanteringsplatser i intranätet kan klientinventeringsdata och insamlade filer skickas osignerade och okrypterade. Kontrollera att platsen har konfigurerats att kräva signering och använda kryptering. Och om klienterna stöder SHA-256-algoritmen väljer du det alternativet så att SHA-256 krävs.|  
|Använd inte filinsamling för att samla in viktiga filer eller känslig information|Configuration Manager program varu inventeringen använder alla behörigheter för LocalSystem-kontot som kan samla in kopior av viktiga systemfiler, till exempel registret eller säkerhets konto databasen. Om dessa filer är tillgängliga på platsservern kan någon som har behörigheten Läs resurs eller NTFS-rättigheter till platsen för de lagrade filerna analysera innehållet och få fram viktig information om klienten som kan äventyra säkerheten.|  
|Begränsa lokala administrativa rättigheter på klientdatorer|En användare med lokal administratörsbehörighet kan skicka ogiltiga data som inventeringsinformation.|  

### <a name="security-issues-for-software-inventory"></a>Säkerhetsproblem för programvaruinventering  
 Insamlingen av inventeringsdata medför potentiella säkerhetsproblem. Angripare kan göra följande:  

- Skicka ogiltiga data som accepteras av hanteringsplatsen även om klientinställningen för programvaruinventering är inaktiverad och filinsamling inte är aktiverat.  

- Skicka för stora mängder data i en enda fil och i massor av filer, vilket kan orsaka en överbelastningsattack (Denial of Service, DoS).  

- Åtkomst till inventerings information när den överförs till Configuration Manager.  

  Om användarna vet att de kan skapa en dold fil med namnet **Skpswi.dat** och placera den i roten på hårddisken för en klient så att klienten undantas från programinventeringen, kan du inte samla in programinventeringsdata från den datorn.  

  Eftersom en användare med lokal administratörs behörighet kan skicka information som inventerings data ska du inte beakta inventerings data som samlas in av Configuration Manager som ska vara auktoritativa.  

  Programvaruinventering är aktiverat som standard som en klientinställning.  

##  <a name="privacy-information-for-software-inventory"></a><a name="BKMK_Privacy_HardwareInventory"></a> Sekretessinformation för programvaruinventering  
 Med maskin varu inventering kan du hämta information som lagras i registret och i WMI på Configuration Manager klienter. Med programvaruinventering kan du identifiera alla filer av en angiven typ eller samla in angivna filer från klienter. Tillgångsinformation förbättrar inventeringsfunktionerna genom att utöka maskin- och programvaruinventeringen och lägga till nya licenshanteringsfunktioner.  

 Maskinvaruinventering är aktiverat som standard som en klientinställning och vilken WMI-information som samlas in beror på vilka alternativ du väljer. Programvaruinventering är aktiverat som standard men filer samlas inte in som standard. Datainsamling för Tillgångsinformation aktiveras automatiskt, men du kan välja vilka rapportklasser för maskinvaruinventering som ska aktiveras.  

 Inventeringsinformation skickas inte till Microsoft. Inventerings information lagras i Configuration Manager-databasen. När klienter använder HTTPS för att ansluta till hanteringsplatser är de inventeringsdata som de skickar till platsen krypterade under överföringen. Om klienter ansluter till hanteringsplatser via HTTP kan du välja att aktivera kryptering av inventeringar. Inventeringsdata sparas inte i krypterat format i databasen. Informationen sparas i databasen tills den raderas av platsunderhållsåtgärderna **Ta bort föråldrad lagerhistorik** eller **Ta bort föråldrade insamlade filer** var 90:e dag. Du kan konfigurera borttagningsintervallet.  

 Innan du konfigurerar maskinvaruinventering, programvaruinventering, filinsamling eller datainsamling för Tillgångsinformation bör du tänka igenom dina sekretesskrav.  
