---
title: Tillgångsinformation säkerhets sekretess
titleSuffix: Configuration Manager
description: Hämta information om säkerhet och sekretess för Tillgångsinformation i Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d0c6f7a0-dcae-4e6d-aa28-35d464d97ff7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3cf35b050b110c655ac85e82a7990f9ea2ac3636
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714145"
---
# <a name="security-and-privacy-for-asset-intelligence-in-configuration-manager"></a>Säkerhet och sekretess för Tillgångsinformation i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Det här avsnittet innehåller information om säkerhet och sekretess för Tillgångsinformation i Configuration Manager.  

##  <a name="security-best-practices-for-asset-intelligence"></a><a name="BKMK_Security_AI"></a> Rekommenderade säkerhetsmetoder för tillgångsinformation  
 Följ dessa rekommenderade säkerhetsmetoder när du använder tillgångsinformation.  

|Regelverk för säkerhet|Mer information|  
|----------------------------|----------------------|  
|När du importerar en licensfil (Microsoft-volymlicensfil eller en allmän licensöversiktsfil) bör du skydda filen och kommunikationskanalen.|Använd NTFS-filsystembehörigheter för att säkerställa att endast behöriga användare har åtkomst till licensfiler, och använd SMB-signering (Server Message Block) för att skydda integriteten för de data som överförs till platsservern under importen.|  
|Använd principen för minsta möjliga behörighet när du importerar licensfiler.|Använd rollbaserad administration för att ge behörighet för att hantera tillgångsinformation till den administrativa användaren som importerar licensfiler. Den inbyggda rollen Tillgångsansvarig omfattar den behörigheten.|  

##  <a name="privacy-information-for-asset-intelligence"></a><a name="BKMK_Privacy_HardwareInventory"></a> Sekretessinformation för tillgångsinformation  
 Tillgångsinformation utökar inventerings funktionerna i Configuration Manager för att ge en högre nivå av till gångs synlighet i företaget. Informationsinsamlingen i Tillgångsinformation aktiveras inte automatiskt. Du kan ändra den typ av information som samlas in genom att aktivera rapporteringsklasser för maskinvaruinventering. Mer information finns i [konfigurera tillgångsinformation](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

 Tillgångsinformation information lagras i Configuration Manager-databasen på samma sätt som inventerings information. När klienter ansluter till hanteringsplatser via HTTPS krypteras alltid data under överföringen till hanteringsplatsen. När klienter ansluter via HTTP kan du ange att inventeringsdataöverföringen ska signeras och krypteras. Inventeringsdata sparas inte krypterat format i databasen. Informationen sparas i databasen tills den raderas av platsunderhållsaktiviteten **Ta bort föråldrad lagerhistorik** , vilket sker var 90:e dag. Du kan konfigurera borttagningsintervallet.  

 Tillgångsinformation skickar ingen information om användare och datorer eller licensanvändning till Microsoft. Du kan välja att skicka System Center Online-förfrågningar för kategorisering vilket innebär att du kan tagga en eller flera okategoriserade programvarutitlar och skicka dem till System Center Online för forskning och kategorisering. När en programvarutitel har laddats upp identifierar och kategoriseras den av Microsoft-personal som också tillgängliggör informationen för alla andra kunder som använder onlinetjänsten. Du bör vara medveten om följande sekretessaspekter när du skickar information till System Center Online:  

- Uppladdning avser endast allmän information om programvarutitlar (namn, utgivare o.s.v.) som du väljer att skicka till System Center Online. Inventeringsinformation skickas inte under en uppladdning.  

- Uppladdning sker aldrig upp automatiskt och systemet är inte heller utformat för att automatisera den aktiviteten. Du måste manuellt välja och godkänna överföring av varje programvarutitel.  

- En dialogruta visar exakt vilka data som kommer att laddas upp innan uppladdningen startar.  

- Licensinformation skickas inte till Microsoft. Licens informationen lagras i ett separat utrymme i Configuration Manager-databasen och kan inte skickas till Microsoft.  

- Alla programvarutitlar som laddas upp blir offentliga i den mening att informationen om ett program och dess kategorisering läggs till i katalogen System Center Online Tillgångsinformation och kan sedan laddas ned av andra som använder katalogen.  

- Källan till programvarutiteln registreras inte i tillgångsinformationskatalogen och är inte heller tillgänglig för andra kunder. Du bör dock kontrollera att du inte laddar upp programtitlar som innehåller privat information.  

- Data som har överförts kan inte återkallas.  

  Innan du ställer in insamling av tillgångsinformationsdata och bestämmer huruvida du ska skicka information till System Center Online bör du tänka på vilka sekretesskrav som finns i din organisation.  
