---
title: Rekommenderad maskinvara
titleSuffix: Configuration Manager
description: Få rekommendationer för maskin vara som hjälper dig att skala din Configuration Manager miljö bortom en grundläggande distribution.
ms.date: 05/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5267f0af-34d3-47a0-9ab8-986c41276e6c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 36b90627f25c5cf19b867a78e141b69266478c58
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428790"
---
# <a name="recommended-hardware-for-configuration-manager"></a>Rekommenderad maskinvara för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Följande rekommendationer är rikt linjer som hjälper dig att skala din Configuration Manager-miljö så att den stöder mer än en mycket grundläggande distribution av platser, plats system och klienter. De är inte avsedda att gälla för alla möjliga konfigurationer av webbplats och hierarki.  

Använd informationen i följande avsnitt som vägledning som hjälper dig att planera för maskin vara. Kontrol lera att maskin varan kan uppfylla bearbetnings belastningen för klienter och platser som använder de tillgängliga Configuration Manager funktionerna.

Mer information finns i [fakta bladet om Configuration Manager prestanda-och skalnings vägledning](https://gallery.technet.microsoft.com/Configuration-Manager-ba55428e).

## <a name="site-systems"></a><a name="bkmk_ScaleSieSystems"></a>Plats system

Det här avsnittet innehåller rekommenderade maskinvarukonfigurationer för Configuration Manager-plats system. Använd de här rekommendationerna för att stödja det maximala antalet klienter och använda de flesta eller alla Configuration Manager funktionerna. Om din miljö har stöd för mindre än det maximala antalet klienter och inte använder alla tillgängliga funktioner kan det kräva mindre resurser. I allmänhet är följande viktiga faktorer begränsat prestanda för det övergripande systemet:

1. Diskens I/O-prestanda

2. Tillgängligt minne

3. Processor

För bästa prestanda använder du RAID 10-konfigurationer för alla data enheter och ett Ethernet-nätverk på 1 Gbit/s.

### <a name="site-servers"></a><a name="bkmk_ScaleSiteServer"></a>Plats servrar

|Plats konfiguration|PROCESSOR (kärnor)|Minne (GB)|Minnesallokering för SQL Server (%)|  
|-------------------------------|---------------|---------------|----------------------------------------|  
|Fristående primär plats server med en databas plats roll på samma server <sup> [anteckning 1](#bkmk_note1)</sup>|16|96|80|  
|Fristående primär plats med en fjärransluten platsdatabas|8|16|-|  
|Fjärransluten databasserver för en fristående primär plats|16|72|90|  
|Central administrations plats server med en databas plats roll på samma server <sup> [anteckning 1](#bkmk_note1)</sup>|20|128|80|  
|Central administrationsplatsserver med en fjärransluten platsdatabas|8|16|-|  
|Fjärransluten databasserver för en central administrationsplats|16|96|90|  
|Underordnad primär plats med en databas plats roll på samma server|16|96|80|  
|Underordnad primär platsserver med en fjärransluten platsdatabas|8|16|-|  
|Fjärransluten databasserver för en underordnad primär plats|16|72|90|  
|Sekundär platsserver|8|16|-|  

#### <a name="note-1-collocated-sql"></a><a name="bkmk_note1"></a>Anmärkning 1: samordnad SQL

När du installerar plats servern och SQL Server på samma dator, stöder distributionen de maximala [storleks-och skalnings numren](size-and-scale-numbers.md) för platser och klienter. Den här konfigurationen kan begränsa [alternativ för hög tillgänglighet](../../servers/deploy/configure/high-availability-options.md), som att använda ett SQL Server-kluster. Om du har en större miljö, på grund av de högre I/O-kraven för att stödja båda rollerna på samma dator, bör du överväga att använda en fjärran sluten SQL Server.

### <a name="remote-site-system-servers"></a><a name="bkmk_RemoteSiteSystem"></a>Fjärrplatsens system servrar

Följande rikt linjer gäller för datorer som har en enda plats system roll. Planera när du installerar flera plats system roller på samma dator.

|Platssystemroll|PROCESSOR (kärnor)|Minne (GB)|Diskutrymme (GB)|  
|----------------------|---------------|---------------|--------------------|  
|Hanteringsplats|4|8|50|  
|Distributionsplats|2|8|Efter vad som krävs av operativ systemet och för att lagra innehåll som du distribuerar|  
|Program uppdaterings plats <sup> [anteckning 2](#bkmk_note2)</sup>|8|16|Efter vad som krävs av operativ systemet och för att lagra uppdateringar som du distribuerar|  
|Alla andra platssystemroller|4|8|50|  

#### <a name="note-2-wsus-configurations"></a><a name="bkmk_note2"></a>Anmärkning 2: WSUS-konfigurationer

Datorn som är värd för en program uppdaterings plats kräver följande konfigurationer för IIS-programpooler:  

- Öka **WsusPool-köns längd** till **2000**.  

- Öka **WsusPool-gränsen för privat minne** med fyra gånger eller ange **0** (obegränsat).  

### <a name="disk-space-for-site-systems"></a><a name="bkmk_DiskSpace"></a>Disk utrymme för plats system

Diskallokering och konfiguration bidrar till prestanda för Configuration Manager. Eftersom varje Configuration Manager miljö är olika kan värdena som du implementerar skilja sig från följande rikt linjer.

Placera varje objekt på en separat, dedikerad RAID-volym för bästa prestanda. För alla data volymer för Configuration Manager och dess databasfiler använder du RAID 10 för bästa prestanda.

|Dataanvändning|Minimalt diskutrymme|25,000 klienter|50,000 klienter|100,000 klienter|150 000 klienter|700 000 klienter (Central administrations webbplats)|  
|----------------|------------------------|--------------------|--------------------|---------------------|---------------------|-----------------------------------------------------|  
|Configuration Manager program-och loggfiler|25 GB|50 GB|100 GB|200 GB|300 GB|200 GB|  
|Platsdatabasens .mdf-fil|75 GB per 25 000 klienter|75 GB|150 GB|300 GB|500 GB|2 TB|  
|Platsdatabasens .ldf-fil|25 GB per 25 000 klienter|25 GB|50 GB|100 GB|150 GB|100 GB|  
|Tillfälliga databasfiler (.mdf och .ldf)|Efter behov|Efter behov|Efter behov|Efter behov|Efter behov|Efter behov|  

För Windows-systemdisken, se storleks vägledning för den installerade OS-versionen.

För innehåll på distributions platser beror det på dina distributioner. Den här vägledningen omfattar inte det disk utrymme som krävs för innehålls biblioteket på plats servern eller distributions platserna. Mer information finns i [innehålls biblioteket](../../../core/plan-design/hierarchy/the-content-library.md).

Tänk på följande rikt linjer när du planerar disk utrymmes kraven:

- Varje klient kräver cirka 5-10 MB utrymme i databasen. Antalet beror på hierarkins typ, konfigurationen och antalet klienter. Storleken är vanligt vis mindre för större miljöer. Mindre platser har större databas användning per klient.<!-- SCCMDocs#1048 -->

- För den primära platsens Temp-databas planerar du för en kombinerad storlek som är 25% till 30% av plats databasens. mdf-fil. Den faktiska storleken kan vara mindre eller större. Det beror på plats serverns prestanda och volymen inkommande data under både korta och långa tids perioder.

  > [!NOTE]
  > När du har 50 000 eller fler klienter på en plats bör du planera att använda fyra eller fler. MDF-filer för den tillfälliga databasen.

- Den tillfälliga databas storleken för en central administrations plats är normalt mycket mindre än för en primär plats.

- Om du använder SQL Server Express för den sekundära plats databasen begränsar den databas storleken till 10 GB.

## <a name="clients"></a><a name="bkmk_ScaleClient"></a>Klienter

Det här avsnittet innehåller rekommenderade maskinvarukonfigurationer för datorer som du hanterar med hjälp av Configuration Manager-klient program vara.

### <a name="client-for-windows-computers"></a>Klient för Windows-datorer

Följande minimi krav gäller för Windows-baserade datorer som du hanterar med hjälp av Configuration Manager, inklusive inbäddade versioner:

- **Processor och minne:** Se processor-och RAM-kraven för operativ systemet.

- **Disk utrymme:** 500 MB ledigt disk utrymme, med 5 GB rekommenderas för Configuration Manager-klientcachen. Om du använder anpassade inställningar för att installera Configuration Manager-klienten krävs mindre disk utrymme.

  - Använd client. msi-egenskapen **SMSCACHESIZE** för att ange en cachestorlek som är mindre än standard storleken på 5120 MB. Den minsta storleken är 1 MB. I följande exempel skapas en cache på 2 MB:`CCMSetup.exe SMSCACHESIZE=2`

    Mer information finns i [om klient installations egenskaper](../../../core/clients/deploy/about-client-installation-properties.md).

    > [!TIP]
    > Det kan vara bra att installera klienten med det minsta diskutrymmet för Windows Embedded-enheter som ofta har mindre diskstorlekar än Windows-standarddatorer.

Följande ytterligare minsta maskin varu krav är för valfria funktioner i Configuration Manager:

- **OS-distribution:** Minst 384 MB RAM-minne

- **Software Center:** Minst en processor på 500 MHz

- **Fjärr styrning:** För en optimal upplevelse, minst en Pentium 4 Hyper-threaded 3 GHz (enkel kärna) eller jämförbar processor, med minst 1 GB RAM-minne.

### <a name="client-for-linux-and-unix"></a>Klienter för Linux och UNIX

Följande minimi krav gäller för Linux-och UNIX-servrar som du hanterar med Configuration Manager.

|Krav|Information|  
|-----------------|-------------|  
|Processor och minne|Se processor-och RAM-kraven för datorns operativ system.|  
|Diskutrymme|500 MB ledigt disk utrymme, med 5 GB rekommenderas för Configuration Manager-klientcachen.|  
|Nätverksanslutningar|Configuration Manager klient datorer måste ha nätverks anslutning till Configuration Manager-plats system för att aktivera hantering.|  

## <a name="configuration-manager-console"></a><a name="bkmk_ScaleConsole"></a>Configuration Manager-konsol

Följande minsta maskin varu krav gäller för varje dator som kör Configuration Manager-konsolen:

- Intel i3 eller jämförbar processor  

- 2 GB RAM  

- 2 GB disk utrymme  

|DPI-inställning|Minsta upplösning|  
|-----------------|------------------------|  
|96/100 %|1024 × 768|  
|120 /125 %|1280 x 960|  
|144/150 %|1600 × 1200|  
|196/200 %|2500 x 1600|  

## <a name="lab-deployments"></a><a name="bkmk_ScaleLab"></a>Labb distributioner

Använd följande minsta maskin varu rekommendationer för labb-och test distributioner av Configuration Manager. De här rekommendationerna gäller för alla plats typer, upp till 100 klienter:  

|Roll|PROCESSOR (kärnor)|Minne (GB)|Diskutrymme (GB)|  
|----------|---------------|-------------------|-----------------------|  
|Plats- och databasserver|2–4|8 - 12|100|  
|Platssystemserver|1–4|2–4|50|  
|Client|1–2|1–3|30|  
