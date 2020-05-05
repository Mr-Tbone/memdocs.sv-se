---
title: Övervaka innehåll
titleSuffix: Configuration Manager
description: Lär dig hur du övervakar distribuerat innehåll med hjälp av Configuration Manager-konsolen.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 82e8a693-9adf-4ca3-8484-7e101c34c7c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fafcbffe3231af78ae3a079061accc9f112a181c
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110023"
---
# <a name="monitor-content-you-distribute-with-configuration-manager"></a>Övervaka innehåll som du distribuerar med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Använd Configuration Manager-konsolen för att övervaka distribuerat innehåll, inklusive:  

- Status för alla paket typer för de associerade distributions platserna.  
- Innehålls validerings status för innehållet i ett paket.  
- Status för innehåll som har tilldelats till en viss distributions plats grupp.  
- Status för innehåll som har tilldelats till en distributions plats.  
- Status för valfria funktioner för varje distributions plats (innehålls validering, PXE och multicast).  

> [!NOTE]  
> Configuration Manager övervakar bara innehållet på en distributions plats som finns i innehålls biblioteket. Det övervakar inte innehåll som lagras på distributions platsen i paket eller anpassade resurser.  

## <a name="content-status-monitoring"></a><a name="BKMK_ContentStatus"></a> Övervakning av innehållsstatus

Noden **Innehållsstatus** i arbetsytan **Övervakning** innehåller information om innehållspaket. I Configuration Manager-konsolen granskar du information som:  

- Paket namn, typ och ID
- Hur många distributions platser ett paket har skickats till
- Frekvens för efterlevnad
- När paketet skapades
- Käll version

Du hittar också detaljerad statusinformation för alla paket, inklusive:  

- Distributions status
- Antalet felaktiga försök
- Väntande distributioner  
- Antalet installationer

Du kan också hantera distributioner som fortfarande pågår till en distributions plats, eller som inte lyckades distribuera innehåll till en distributions plats:  

- Alternativet att antingen avbryta eller omdistribuera innehållet är tillgängligt när du visar distributions status meddelandet för ett distributions jobb till en distributions plats i fönstret **till gångs information** . Du hittar den här rutan på fliken **pågår** eller fliken **fel** i noden **innehålls status** .  
- Dessutom visar jobb informationen den procent andel av jobbet som har slutförts när du visar information om ett jobb på fliken **pågår** . Jobb informationen visar också antalet återförsök som är kvar för ett jobb. När du visar information om ett jobb på fliken **fel** visas hur lång tid det tar innan nästa försök görs.  

När du avbryter en distribution som inte har slutförts, stoppas distributions jobbet för att överföra innehållet:  

- Statusen för distributionen uppdateras sedan för att indikera att distributionen misslyckades och att den avbröts av en användar åtgärd.  
- Den nya statusen visas på fliken **fel** .  

> [!NOTE]  
> När en distribution är nära slutförd, är det möjligt att avbryta distributionen och inte bearbeta den innan distributionen till distributions platsen har slutförts. När detta inträffar ignoreras åtgärden att avbryta distributionen och statusen för distributionen visas som slutförd.  
>
> Även om du kan välja alternativet att avbryta en distribution till en distributions plats som finns på en plats Server, har detta ingen påverkan. Det här problemet beror på att plats servern och distributions platsen på en plats Server delar samma innehålls lagring för en enda instans. Det finns inget verkligt distributions jobb att avbryta.  

När du distribuerar om innehåll som tidigare inte gick att överföra till en distributions plats börjar Configuration Manager omedelbart omdistribuera innehållet till distributions platsen. Configuration Manager uppdaterar statusen för distributionen för att återspegla det pågående tillståndet för distributionen.  

### <a name="tasks-to-monitor-content"></a>Aktiviteter för att övervaka innehåll

1. I Configuration Manager-konsolen går du till arbets ytan **övervakning** , expanderar **distributions status**och väljer sedan noden **innehålls status** . Den här noden visar paketen.  

2. Välj det paket som du vill hantera.  

3. På fliken **Start** i menyfliksområdet väljer du **Visa status**i gruppen **innehåll** . I-konsolen visas detaljerad statusinformation för paketet.

Fortsätt till något av följande avsnitt om du vill ha ytterligare åtgärder:

#### <a name="cancel-a-distribution-that-remains-in-progress"></a>Avbryta en distribution som fortfarande pågår  

1. Växla till fliken **pågår** .

2. Högerklicka på posten för den distribution som du vill avbryta i fönstret **till gångs information** och välj **Avbryt**.  

3. Välj **Ja** för att bekräfta åtgärden och avbryta distributions jobbet till distributions platsen.  

#### <a name="redistribute-content-that-failed-to-distribute"></a>Distribuera om innehåll som inte kunde distribueras  

1. Växla till fliken **fel** .

2. I fönstret **till gångs information** högerklickar du på posten för den distribution som du vill distribuera om och väljer **omdistribuera**.  

3. Välj **Ja** för att bekräfta åtgärden och starta omdistributions processen till den distributions platsen.  


## <a name="distribution-point-group-status"></a>Gruppstatus för distributionsplatser

Noden **Gruppstatus för distributionsplatser** på arbetsytan **Övervakning** innehåller information om distributionsplatsgrupper. Du kan granska information som:  

- Distributions plats gruppens namn, beskrivning och status
- Hur många distributions platser är medlemmar i distributions plats gruppen
- Hur många paket som har tilldelats gruppen
- Frekvensen för efterlevnad

Du ser även följande detaljerade statusinformation:  

- Fel för distributions plats gruppen  
- Hur många distributioner som pågår
- Hur många distributioner som har distribuerats  

### <a name="monitor-distribution-point-group-status"></a>Övervaka distributions plats gruppens status  

1. I Configuration Manager-konsolen går du till arbets ytan **övervakning** , expanderar **distributions status**och väljer sedan noden **distributions plats grupp status** . Den visar distributions plats grupper.  

2. Välj den distributions plats grupp som du vill ha detaljerad statusinformation om.  

3. På fliken **Start** i menyfliksområdet väljer du **Visa status**. Den visar detaljerad statusinformation för distributions plats gruppen.  


## <a name="distribution-point-configuration-status"></a>Konfigurationsstatus för distributionsplatser

Noden **Konfigurationsstatus för distributionsplatser** på arbetsytan **Övervakning** innehåller information om distributionsplatsen. Du kan granska vilka attribut som är aktiverade för distributions platsen, till exempel PXE, multicast och innehålls validering. Granska även distributions status för distributions platsen.

> [!WARNING]  
> Distributions platsens konfigurations status är relativ till de senaste 24 timmarna. Om distributions platsen har ett fel och återställningar kan fel statusen visas i upp till 24 timmar efter återställningen av distributions platsen.  

### <a name="monitor-distribution-point-configuration-status"></a>Övervaka konfigurations status för distributions platser  

1. I Configuration Manager-konsolen går du till arbets ytan **övervakning** , expanderar **distributions status**och väljer sedan noden **konfigurations status för distributions plats** .  

2. Välj en distributions plats.  

3. I resultat fönstret växlar du till fliken **information** . Den visar status information för distributions platsen.  


## <a name="client-data-sources-dashboard"></a>Instrument panel för klient data källor

Använd instrument panelen för **klient data källor** för att få bättre förståelse för hur klienter hämtar innehåll i din miljö. Instrument panelen börjar visa data efter att-klienter laddar ned innehåll och rapporterar informationen tillbaka till webbplatsen. Den här processen kan ta upp till 24 timmar.

> [!Note]  
> Configuration Manager aktiverar inte den här valfria funktionen som standard. Du måste aktivera funktionen **klient-peer-cache** innan du använder den. Mer information finns i avsnittet [Enable optional features from updates](../../manage/install-in-console-updates.md#bkmk_options).  

I Configuration Manager-konsolen går du till arbets ytan **övervakning** , expanderar **distributions status**och väljer noden **klient data källor** . Välj en tids period som ska tillämpas på instrument panelen. Välj sedan den avgränsnings grupp som du vill visa information om. Du kan hovra över paneler för att se mer information om de olika innehålls-eller princip källorna.

Använd också rapporten, **klient data källor – Sammanfattning**för att visa en sammanfattning av klient data källorna för varje avgränsnings grupp.

### <a name="dashboard-tiles"></a>Paneler på instrumentpanelen

Instrument panelen innehåller följande paneler:  

#### <a name="client-content-sources"></a>Klient innehålls källor

Visar de källor från vilka klienterna fick innehåll:

- Distributionsplats
- [Moln distributions plats](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)
- [BranchCache](../../../plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache)
- [Peer-cache](../../../plan-design/hierarchy/client-peer-cache.md)
- [Leverans optimering](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization) (från och med version 1906)<sup>[Anmärkning 1](#bkmk_note1)</sup>
- Microsoft Update: enheter rapporterar den här källan när Configuration Manager klienten laddar ned program uppdateringar från Microsoft Cloud Services. Dessa tjänster omfattar Microsoft Update och Microsoft 365 appar för företag.

![Panelen klient innehålls källor på instrument panelen](media/3555759-do-source.png)

<a name="bkmk_note1"></a>

> [!Note]  
> Från och med version 1906<!--3555759-->, om du vill inkludera leverans optimering på den här instrument panelen gör du följande:
>
> - Konfigurera klient inställningen, **Aktivera installation av Express uppdateringar på klienter** i program uppdaterings gruppen
>
> - Distribuera Windows 10 Express-uppdateringar
>
> Mer information finns i [Hantera snabb installationsfiler för Windows 10-uppdateringar](../../../../sum/deploy-use/manage-express-installation-files-for-windows-10-updates.md).

#### <a name="distribution-points"></a>Distributionsplatser

Visar antalet distributions platser som ingår i den valda gränser gruppen.

#### <a name="clients-that-used-a-distribution-point"></a>Klienter som använde en distributions plats

För det antal klienter som finns i den valda gränser gruppen visar den här panelen hur många som använder en distributions plats för att hämta innehåll.

#### <a name="peer-cache-sources"></a>Peer-cache-källor

Den här panelen visar hur många peer cache-källor som har rapporterat nedladdnings historiken för den valda gränser gruppen.

#### <a name="clients-that-used-a-peer"></a>Klienter som har använt en peer

För antalet klienter som finns i den valda gränser-gruppen visar den här panelen hur många som använder en peer-cache-källa för att hämta innehåll.

#### <a name="top-distributed-content"></a>Översta distribuerade innehållet

De mest distribuerade paketen efter källtyp
