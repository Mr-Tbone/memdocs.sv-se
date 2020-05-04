---
title: Säkerhets sekretess för maskin varu inventering
titleSuffix: Configuration Manager
description: Hämta information om säkerhet och sekretess för maskin varu inventering i Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 62e20d86-db6d-4a1f-b14a-905a9de31698
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a5989c80818ac45bb8dd6a4f768595dbd56b846d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710687"
---
# <a name="security-and-privacy-for-hardware-inventory-in-configuration-manager"></a>Säkerhet och sekretess för maskin varu inventering i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Det här avsnittet innehåller information om säkerhet och sekretess för maskin varu inventering i Configuration Manager.  

##  <a name="security-best-practices-for-hardware-inventory"></a><a name="BKMK_Security_HardwareInventory"></a> Rekommenderade säkerhetsmetoder för maskinvaruinventering  
 Använd följande rekommenderade säkerhetsmetoder när du samlar in maskinvaruinventeringsdata från klienter:  

|Regelverk för säkerhet|Mer information|  
|----------------------------|----------------------|  
|Signera och kryptera inventeringsdata|När klienterna kommunicerar med hanteringsplatser med hjälp av HTTPS krypteras alla data som de skickar med hjälp av SSL. Men när klientdatorer använder HTTP för att kommunicera med hanteringsplatser i intranätet kan klientinventeringsdata och insamlade filer skickas osignerade och okrypterade. Kontrollera att platsen har konfigurerats att kräva signering och använda kryptering. Och om klienterna stöder SHA-256-algoritmen väljer du det alternativet så att SHA-256 krävs.|  
|Samla inte in IDMIF- och NOIDMIF-filer i miljöer med hög säkerhet|Du kan använda samlingen med IDMIF- och NOIDMIF-filer för att utöka maskinvarusamlingen. Vid behov skapar Configuration Manager nya tabeller eller ändrar befintliga tabeller i Configuration Manager-databasen för att hantera egenskaperna i IDMIF-och NOIDMIF-filer. Men Configuration Manager validerar inte IDMIF-och NOIDMIF-filer, så dessa filer kan användas för att ändra tabeller som du inte vill ska ändras. Giltiga data kan skrivas över av ogiltiga data. Dessutom kan stora mängder data läggas till och bearbetningen av dessa data kan orsaka fördröjningar i alla Configuration Manager funktioner. För att undvika detta ställer du in klientinställningen **Samla in MIF-filer** för maskinvarukonfigurationen på **Inga**.|  

### <a name="security-issues-for-hardware-inventory"></a>Säkerhetsproblem för maskinvaruinventering  
 Insamlingen av inventeringsdata medför potentiella säkerhetsproblem. Angripare kan göra följande:  

- Skicka ogiltiga data som accepteras av hanteringsplatsen även om klientinställningen för programvaruinventering är inaktiverad och filinsamling inte är aktiverat.  

- Skicka för stora mängder data i en enda fil och i massor av filer, vilket kan orsaka en överbelastningsattack (Denial of Service, DoS).  

- Åtkomst till inventerings information när den överförs till Configuration Manager.  

  Eftersom en användare med lokal administratörs behörighet kan skicka information som inventerings data ska du inte beakta inventerings data som samlas in av Configuration Manager som ska vara auktoritativa.  

  Maskinvaruinventering är aktiverat som standard som en klientinställning.  

##  <a name="privacy-information-for-hardware-inventory"></a><a name="BKMK_Privacy_HardwareInventory"></a> Sekretessinformation för maskinvaruinventering  
 Med maskin varu inventering kan du hämta information som lagras i registret och i WMI på Configuration Manager klienter. Med programvaruinventering kan du identifiera alla filer av en angiven typ eller samla in angivna filer från klienter. Tillgångsinformation förbättrar inventeringsfunktionerna genom att utöka maskin- och programvaruinventeringen och lägga till nya licenshanteringsfunktioner.  

 Maskinvaruinventering är aktiverat som standard som en klientinställning och vilken WMI-information som samlas in beror på vilka alternativ du väljer. Programvaruinventering är aktiverat som standard men filer samlas inte in som standard. Datainsamling för Tillgångsinformation aktiveras automatiskt, men du kan välja vilka rapportklasser för maskinvaruinventering som ska aktiveras.  

 Inventeringsinformation skickas inte till Microsoft. Inventerings information lagras i Configuration Manager-databasen. När klienter använder HTTPS för att ansluta till hanteringsplatser är de inventeringsdata som de skickar till platsen krypterade under överföringen. Om klienter ansluter till hanteringsplatser via HTTP kan du välja att aktivera kryptering av inventeringar. Inventeringsdata sparas inte i krypterat format i databasen. Informationen sparas i databasen tills den raderas av platsunderhållsåtgärderna **Ta bort föråldrad lagerhistorik** eller **Ta bort föråldrade insamlade filer** var 90:e dag. Du kan konfigurera borttagningsintervallet.  

 Innan du konfigurerar maskinvaruinventering, programvaruinventering, filinsamling eller datainsamling för Tillgångsinformation bör du tänka igenom dina sekretesskrav.  
