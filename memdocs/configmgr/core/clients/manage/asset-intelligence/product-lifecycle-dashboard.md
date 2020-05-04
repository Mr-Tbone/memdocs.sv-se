---
title: Instrument panel för produkt livs cykel
titleSuffix: Configuration Manager
description: Visa Microsofts livs cykel policy med instrument panelen för produktens livs cykel i Configuration Manager.
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8b5b144a-0e5f-4fcc-87b2-33b9bcdb5655
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 178331865c8f3efd660e4a0037674eed3621fe6b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714243"
---
# <a name="manage-microsoft-lifecycle-policy-with-configuration-manager"></a>Hantera Microsofts livs cykel policy med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Från och med version 1806 kan du använda instrument panelen för Configuration Manager produktens livs cykel för att Visa Microsofts livs cykel princip. På instrument panelen visas statusen för Microsofts livs cykel princip för Microsoft-produkter som är installerade på enheter som hanteras med Configuration Manager. Du får också information om Microsoft-produkter i din miljö, support tillstånd och slutdatum för support. Använd instrument panelen för att förstå tillgängligheten för varje produkt. Den här informationen hjälper dig att planera för när du ska uppdatera de Microsoft-produkter som du använder innan deras aktuella slut på support nås.  

Mer information finns i [Microsofts livs cykel princip](https://support.microsoft.com/lifecycle).

Från och med version 1810 innehåller instrument panelen information om System Center 2012 Configuration Manager och senare.<!--1358702-->  



## <a name="prerequisites"></a>Krav 

 Följande komponenter krävs för att se data i instrument panelen för produktens livs cykel:  

- Internet Explorer 9 eller senare måste vara installerat på datorn som kör Configuration Manager-konsolen.  

- En tjänst anslutnings punkt roll måste vara installerad och konfigurerad. För att hämta uppdateringar för data på den här instrument panelen måste tjänst anslutnings punkten vara online eller synkroniseras regelbundet om den är offline. Mer information finns i [om tjänst anslutnings punkten](../../../servers/deploy/configure/about-the-service-connection-point.md).

- En repor ting Services-plats krävs för HYPERLINK-funktioner på instrument panelen. Instrument panelen Länkar till SQL Server Reporting Services rapporter (SSRS). Mer information finns i [Introduktion till rapportering](../../../servers/manage/introduction-to-reporting.md).  

- Platsen för synkronisering av till gångs information måste konfigureras och synkroniseras. På instrument panelen används till gångs informations katalogen som metadata för produkt titlar. Metadata jämförs med inventerings data i hierarkin. Mer information finns [i Konfigurera till gångs information i Configuration Manager](configuring-asset-intelligence.md).  
  - Om du konfigurerar till gångs informations tjänsten för första gången, se till att [Aktivera maskin varu lager klasser för till gångs information](configuring-asset-intelligence.md#BKMK_EnableAssetIntelligence). Instrument panelens livs cykel är beroende av maskin varu lager klasserna för till gångs information. Instrument panelen visar inte data förrän klienterna har sökt efter och returnerat maskin varu inventering.  
  - Om du vill visa information om utökade säkerhets uppdateringar (ESU) på den här instrument panelen aktiverar du **produkt tillgångsinformation (produkt)** för maskin varu inventerings klass. Mer information finns i [Aktivera maskin varu lager klasser för till gångs information](configuring-asset-intelligence.md#BKMK_EnableAssetIntelligence). <!--4962901-->



## <a name="use-the-product-lifecycle-dashboard"></a>Använd instrument panelen för produktens livs cykel

Baserat på inventerings data som webbplatsen samlar in från hanterade enheter, visar instrument panelen information om alla aktuella produkter. Informationen som visas för operativ system och SQL Server är dock begränsad till följande versioner:

- Windows Server 2008 och senare
- Windows XP och senare
- SQL Server 2008 och senare

För att komma åt instrument panelen för livs cykeln i Configuration Manager-konsolen går du till arbets ytan **till gångar och efterlevnad** , expanderar **tillgångsinformation**och väljer noden **produktens livs cykel** .

> [!NOTE]  
> Data i instrument panelen baseras på platsen som Configuration Manager-konsolen ansluter till. Om-konsolen ansluter till platsen på den högsta nivån visas data för hela hierarkin. När du är ansluten till en underordnad primär plats visas endast data från den platsen.

### <a name="product-lifecycle-dashboard"></a>Instrument panel för produkt livs cykel

![Skärm bild av instrument panelen för produktens livs cykel i-konsolen](media/product-lifecycle-dashboard.png)

Ändra vyn genom att välja något av följande alternativ i listan **produkt kategori** :  
- **Alla**: Visa alla produkter tillsammans  
- **Windows-klient**: Visa Windows-KLIENTens OS-versioner  
- **Windows Server**: Visa Windows Server OS-versioner  
- **Databas**: Visa SQL Server versioner  
- **Configuration Manager**: startar i version 1810, Visa Configuration Manager versioner 
- **Microsoft Office**: startar i version 1902, Visa information om installerade versioner av Office 2003 via Office 2016 <!--3556026-->

Instrumentpanelen innehåller följande ikoner:  

- De **fem främsta produkterna efter livs längd**: den här panelen är en sammanställd datavy för produkter som finns i din miljö efter deras livs längd. Diagrammet visar installerad program vara som har upphört att gälla jämfört med support livs cykeln för operativ system och SQL Server-produkter.  

- **De fem främsta produkterna närmar sig livs längd**: den här panelen är en sammanslagen datavy för produkter som finns i din miljö som är närmast livs längd under de kommande 18 månaderna. Diagrammet visar installerad program vara som är inom 18 månader från livs längd jämfört med support livs cykeln för operativ system och SQL Server-produkter.  

- **Livs cykel data för installerade produkter**: den här panelen ger dig en allmän uppfattning om när en produkt över gångar från har stöd för förfallet tillstånd. Diagrammet innehåller en uppdelning av antalet klienter där produkten är installerad, Supportens tillgänglighets tillstånd och en länk för att lära dig mer om nästa steg att vidta. Följande information ingår i diagrammet:     
    - Återstående support tid
    - Tal i miljö 
    - Slutdatum för vanlig support
    - Slutdatum för utökad support
    - Nästa steg  

> [!IMPORTANT]  
> Informationen som visas på den här instrument panelen tillhandahålls för din bekvämlighet och används internt i företaget. Du bör inte bara förlita dig på den här informationen för att bekräfta efterlevnad. Se till att kontrol lera att informationen som du har fått är korrekt, tillsammans med support information genom att gå till [Microsofts livs cykel princip](https://support.microsoft.com/lifecycle).  



## <a name="reporting"></a>Rapportering

Ytterligare rapporter är också tillgängliga. I Configuration Manager-konsolen går du till arbets ytan **övervakning** , expanderar **rapportering**och expanderar **rapporter**. Följande nya rapporter läggs till under kategorin **tillgångsinformation**:  

- **Livs cykel 01A – datorer med en specifik program varu produkt**: Visa en lista med datorer där en angiven produkt har identifierats.  

- **Livs cykel 02A – lista över datorer med utgångna produkter i organisationen**: Visa datorer som har förfallit produkter på dem. Du kan filtrera den här rapporten efter produkt namn.

- **Livs cykel 03a – lista över utgångna produkter som finns i organisationen**: Visa information om produkter i din miljö som har förfallit livs cykel datum.  

- **Livs cykel 04A – översikt över generell produkt livs cykel**: Visa en lista med livscykler för produkter. Filtrera listan efter produkt namn och dagar som ska upphöra att gälla.  

- **Livs cykel 05A – instrument panel för produkt livs cykel**: från och med version 1810, innehåller den här rapporten liknande information som instrument panelen i konsolen. Välj en kategori om du vill visa antalet produkter i din miljö och vilka support dagar som återstår.  

Mer information finns i [lista över rapporter](../../../servers/manage/list-of-reports.md#asset-intelligence).<!--SCCMDocs issue 997-->  
