---
title: Rekommenderad maskinvara
titleSuffix: Configuration Manager
description: Få rekommendationer för maskin vara som hjälper dig att skala din Configuration Manager miljö bortom en grundläggande distribution.
ms.date: 05/23/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5267f0af-34d3-47a0-9ab8-986c41276e6c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d741e34325da859d4fe1f0af554544ce146a42f9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719164"
---
# <a name="recommended-hardware-for-configuration-manager"></a>Rekommenderad maskinvara för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Följande rekommendationer är rikt linjer som hjälper dig att skala din Configuration Manager-miljö så att den stöder mer än en mycket grundläggande distribution av platser, plats system och klienter. De här rekommendationerna är inte avsedda att täcka alla möjliga plats- och hierarkikonfigurationer.  

Använd informationen i följande avsnitt som vägledning som hjälper dig att planera för maskin vara som kan uppfylla bearbetnings belastningen för klienter och platser som använder de tillgängliga Configuration Manager funktionerna med standardkonfigurationerna.  



##  <a name="site-systems"></a><a name="bkmk_ScaleSieSystems"></a>Plats system  
Det här avsnittet innehåller rekommenderade maskinvarukonfigurationer för Configuration Manager plats system för distributioner som har stöd för det maximala antalet klienter och som använder de flesta eller alla Configuration Manager-funktioner. Distributioner som har stöd för mindre än det maximala antalet klienter och som inte använder alla tillgängliga funktioner kan kräva färre dator resurser. De viktigaste faktorerna som begränsar den övergripande systemprestandan innefattar följande, i ordning:  

1.  Diskens I/O-prestanda  

2.  Tillgängligt minne  

3.  Processor  

För bästa prestanda använder du RAID 10-konfigurationer för alla data enheter och ett Ethernet-nätverk på 1 Gbit/s.  

###  <a name="site-servers"></a><a name="bkmk_ScaleSiteServer"></a>Plats servrar  

|Plats konfiguration|PROCESSOR (kärnor)|Minne (GB)|Minnesallokering för SQL Server (%)|  
|-------------------------------|---------------|---------------|----------------------------------------|  
|Fristående primär plats server med en databas plats roll på samma server<sup>1</sup>|16|96|80|  
|Fristående primär plats med en fjärransluten platsdatabas|8|16|-|  
|Fjärransluten databasserver för en fristående primär plats|16|72|90|  
|Central administrations plats server med en databas plats roll på samma server<sup>1</sup>|20|128|80|  
|Central administrationsplatsserver med en fjärransluten platsdatabas|8|16|-|  
|Fjärransluten databasserver för en central administrationsplats|16|96|90|  
|Underordnad primär plats med en databas plats roll på samma server|16|96|80|  
|Underordnad primär platsserver med en fjärransluten platsdatabas|8|16|-|  
|Fjärransluten databasserver för en underordnad primär plats|16|72|90|  
|Sekundär platsserver|8|16|-|  

<sup>1</sup> när plats servern och SQL Server är installerade på samma dator har distributionen stöd för högsta [storlek och skalnings nummer](size-and-scale-numbers.md) för platser och klienter. Den här konfigurationen kan dock begränsa [alternativ för hög tillgänglighet för Configuration Manager](../../servers/deploy/configure/high-availability-options.md), som att använda ett SQL Server kluster. På grund av de högre I/O-kraven som krävs för att stödja både SQL Server och Configuration Manager plats servern när du kör båda på samma dator, är det en bra idé att överväga att använda en konfiguration med en fjärran sluten SQL Server dator om du har en större distribution.  

###  <a name="remote-site-system-servers"></a><a name="bkmk_RemoteSiteSystem"></a>Fjärrplatsens system servrar  
Följande rikt linjer gäller för datorer som har en enda plats system roll. Planera för justeringar när du installerar flera platssystemroller på samma dator.  

|Platssystemroll|PROCESSOR (kärnor)|Minne (GB)|Diskutrymme (GB)|  
|----------------------|---------------|---------------|--------------------|  
|Hanteringsplats|4|8|50|  
|Distributionsplats|2|8|Efter vad som krävs av operativ systemet och för att lagra innehåll som du distribuerar|  
|Program uppdaterings punkt<sup>1</sup>|8|16|Efter vad som krävs av operativ systemet och för att lagra uppdateringar som du distribuerar|  
|Alla andra platssystemroller|4|8|50|  

<sup>1</sup> datorn som är värd för en program uppdaterings plats kräver följande konfigurationer för IIS-programpooler:  

- Öka **WsusPool-köns längd** till **2000**.  

- Öka **WsusPool-gränsen för privat minne** med fyra gånger eller ange **0** (obegränsat).  

###  <a name="disk-space-for-site-systems"></a><a name="bkmk_DiskSpace"></a>Disk utrymme för plats system  
Diskallokering och konfiguration bidrar till prestanda för Configuration Manager. Eftersom varje Configuration Manager miljö är olika kan värdena som du implementerar skilja sig från följande rikt linjer.  

Placera varje objekt på en separat, dedikerad RAID-volym för bästa prestanda. För alla data volymer (Configuration Manager och dess databasfiler) använder du RAID 10 för bästa prestanda.  

|Dataanvändning|Minimalt diskutrymme|25,000 klienter|50,000 klienter|100,000 klienter|150 000 klienter|700 000 klienter (Central administrations webbplats)|  
|----------------|------------------------|--------------------|--------------------|---------------------|---------------------|-----------------------------------------------------|  
|Operativsystem|Se anvisningar för operativsystemet.|Se anvisningar för operativsystemet.|Se anvisningar för operativsystemet.|Se anvisningar för operativsystemet.|Se anvisningar för operativsystemet.|Se anvisningar för operativsystemet.|  
|Configuration Manager program-och loggfiler|25 GB|50 GB|100 GB|200 GB|300 GB|200 GB|  
|Platsdatabasens .mdf-fil|75 GB per 25 000 klienter|75 GB|150 GB|300 GB|500 GB|2 TB|  
|Platsdatabasens .ldf-fil|25 GB per 25 000 klienter|25 GB|50 GB|100 GB|150 GB|100 GB|  
|Tillfälliga databasfiler (.mdf och .ldf)|Efter behov|Efter behov|Efter behov|Efter behov|Efter behov|Efter behov|  
|Innehåll (distributionsplatsresurser)|Efter behov<sup>1</sup>|Efter behov<sup>1</sup>|Efter behov<sup>1</sup>|Efter behov<sup>1</sup>|Efter behov<sup>1</sup>|Efter behov<sup>1</sup>|  

<sup>1</sup> disk utrymmes vägledningen innehåller inte det utrymme som krävs för innehåll som finns i innehålls biblioteket på plats servern eller distributions platserna. Information om hur du planerar innehållsbiblioteket finns i [Innehållsbiblioteket](../../../core/plan-design/hierarchy/the-content-library.md).  

Utöver föregående rekommendationer bör du tänka på följande riktlinjer när du planerar diskutrymmeskraven:  

- Varje klient kräver cirka 5 MB utrymme.  

- När du planerar storleken på den tillfälliga databasen för en primär plats bör du planera för en kombinerad storlek som är 25% till 30% av plats databasens. mdf-fil. Den faktiska storleken kan vara betydligt mindre eller större, det beror på plats serverns prestanda och volymen inkommande data under både korta och långa tids perioder.  

  > [!NOTE]  
  >  När du har 50 000 eller fler klienter på en plats bör du planera att använda fyra eller fler. MDF-filer för den tillfälliga databasen.  

- Den tillfälliga databas storleken för en central administrations plats är normalt mycket mindre än för en primär plats.  

- Den sekundära platsens databas har följande storleks begränsningar:  

  - SQL Server 2012 Express: 10 GB  

  - SQL Server 2014 Express: 10 GB  

##  <a name="clients"></a><a name="bkmk_ScaleClient"></a>Klienter  
Det här avsnittet innehåller rekommenderade maskinvarukonfigurationer för datorer som du hanterar med hjälp av Configuration Manager-klient program vara.  

### <a name="client-for-windows-computers"></a>Klient för Windows-datorer  
Följande är minimi kraven för Windows-baserade datorer som du hanterar med hjälp av Configuration Manager, inklusive inbäddade operativ system:  

- **Processor och minne:** Se processor-och RAM-kraven för datorns operativ system.  

- **Disk utrymme:** 500 MB tillgängligt disk utrymme, med 5 GB rekommenderas för Configuration Manager-klientcachen. Mindre disk utrymme krävs om du använder anpassade inställningar för att installera Configuration Manager-klienten:  

    - Använd Client.msi-egenskapen SMSCACHESIZE om du vill ange en cachefil som har en mindre storlek än standardstorleken på 5 120 MB. Den minsta storleken är 1 MB. Till exempel `CCMSetup.exe SMSCachesize=2` skapar en cache som är 2 MB stor.  

    Mer information om dessa klient installations inställningar finns i [om klient installations egenskaper](../../../core/clients/deploy/about-client-installation-properties.md).  

    > [!TIP]  
    > Det kan vara bra att installera klienten med det minsta diskutrymmet för Windows Embedded-enheter som ofta har mindre diskstorlekar än Windows-standarddatorer.  

Följande är ytterligare minsta maskin varu krav för valfria funktioner i Configuration Manager.  

- **Operativ Systems distribution:** 384 MB RAM  

- **Software Center:** 500 MHz processor  

- **Fjärr styrning:** Pentium 4 Hyper-threaded 3 GHz (enkel kärna) eller jämförbar processor, med minst 1 GB RAM för optimal upplevelse  

### <a name="client-for-linux-and-unix"></a>Klienter för Linux och UNIX  
Följande är minimi kraven för Linux-och UNIX-servrar som du hanterar med Configuration Manager.  

|Krav|Information|  
|-----------------|-------------|  
|Processor och minne|Se kraven på processor och RAM för datorns operativ system.|  
|Diskutrymme|500 MB tillgängligt disk utrymme, med 5 GB rekommenderas för Configuration Manager-klientcachen.|  
|Nätverksanslutningar|Configuration Manager klient datorer måste ha nätverks anslutning till Configuration Manager-plats system för att aktivera hantering.|  

##  <a name="configuration-manager-console"></a><a name="bkmk_ScaleConsole"></a>Configuration Manager-konsol  
Kraven i följande tabell gäller för varje dator som kör Configuration Manager-konsolen.  

**Minsta maskinvarukonfiguration:**  

- Intel i3 eller jämförbar processor  

- 2 GB RAM  

- 2 GB disk utrymme  

|DPI-inställning|Minsta upplösning|  
|-----------------|------------------------|  
|96/100 %|1024 × 768|  
|120 /125 %|1280 x 960|  
|144/150 %|1600 × 1200|  
|196/200 %|2500 x 1600|  

**Stöd för PowerShell:**  

När du installerar stöd för PowerShell på en dator som kör Configuration Manager-konsolen kan du köra PowerShell-cmdlets på den datorn för att hantera Configuration Manager.

- PowerShell 3,0 eller senare stöds

Förutom PowerShell stöds Windows Management Framework (WMF) version 3,0 eller senare.   


##  <a name="lab-deployments"></a><a name="bkmk_ScaleLab"></a>Labb distributioner  
Använd följande minsta maskin varu rekommendationer för labb-och test distributioner av Configuration Manager. De här rekommendationerna gäller för alla plats typer, upp till 100 klienter:  

|Roll|PROCESSOR (kärnor)|Minne (GB)|Diskutrymme (GB)|  
|----------|---------------|-------------------|-----------------------|  
|Plats- och databasserver|2–4|8 - 12|100|  
|Platssystemserver|1–4|2–4|50|  
|Klient|1–2|1–3|30|  
