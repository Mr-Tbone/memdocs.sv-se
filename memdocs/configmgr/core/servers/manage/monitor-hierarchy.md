---
title: Övervaka hierarkin
titleSuffix: Configuration Manager
description: Lär dig hur du övervakar infrastrukturen i Configuration Manager med hjälp av arbets ytan övervakning i-konsolen.
ms.date: 06/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 007dbb73-18a7-48a3-a489-97cf9fc4f140
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 66fc6744ef7d1aaf90a5e7339cc9a5174c0d33f6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713704"
---
# <a name="monitor-the-hierarchy"></a>Övervaka hierarkin

*Gäller för: Configuration Manager (aktuell gren)*

Om du vill övervaka din hierarki i Configuration Manager använder du arbets ytan **övervakning** i Configuration Manager-konsolen.  

> [!NOTE]  
> Undantaget till den här platsen är när du migrerar platser. Övervakade den här processen i noden **migrering** i arbets ytan **Administration** . Mer information finns i [åtgärder för att migrera till Configuration Manager aktuella grenen](../../migration/operations-for-migration.md).  

Med hjälp av Configuration Manager-konsolen för övervakning, använder du följande funktioner:

- [Introduktion till rapportering](introduction-to-reporting.md)
- [Loggfiler](../../plan-design/hierarchy/log-files.md).  

När du övervakar platser ska du leta efter tecken på problem som du behöver åtgärda. Ett exempel:  

- Eftersläpande filer på platsservrar och platssystem.  

- Statusmeddelanden som tyder på ett fel eller problem.  

- Misslyckade kommunikationsförsök inom en plats.  

- Fel- och varningsmeddelanden i systemhändelseloggen på servrar.  

- Fel- och varningsmeddelanden i Microsoft SQL Servers fellogg.  

- Platser eller klienter som inte har rapporterat status under en längre tid.  

- En SQL Server-databas som arbetar trögt.  

- Tecken på att maskinvara håller på att gå sönder.  

Om övervaknings aktiviteter avslöjar några tecken på problem kan du undersöka orsaken till problemet. Sedan kan du snabbt reparera den för att minimera risken för att en plats kraschar.  


## <a name="monitor-common-management-tasks"></a><a name="BKMK_MonintorMgmtTasks"></a>Övervaka vanliga hanterings uppgifter

Configuration Manager tillhandahåller inbyggd övervakning i Configuration Manager-konsolen.

### <a name="alerts"></a>Aviseringar

Mer information finns i [Övervaka aviseringar](use-alerts-and-the-status-system.md#BKMK_MonitorAlerts).  

### <a name="compliance-settings"></a>Kompatibilitetsinställningar

Mer information finns i [så här övervakar du](../../../compliance/deploy-use/monitor-compliance-settings.md)kompatibilitetsinställningar.

### <a name="content"></a>Innehåll

Allmän information om att övervaka innehåll finns i [Hantera innehåll och innehålls infrastruktur](../deploy/configure/manage-content-and-content-infrastructure.md).  

Mer information om övervakning av vissa typer av innehåll:

- [Övervakning av program](../../../apps/deploy-use/monitor-applications-from-the-console.md)

- [Övervaka paket och program](../../../apps/deploy-use/packages-and-programs.md#monitor-packages-and-programs)  

- [Övervaka innehåll för program uppdateringar](../../../sum/deploy-use/monitor-software-updates.md#BKMK_MonitorContent)

- [Övervaka innehåll för OS-distributioner](../../../osd/deploy-use/monitor-operating-system-deployments.md#BKMK_MonitorContent)

### <a name="endpoint-protection"></a>Slutpunktsskydd

Mer information finns i [så här övervakar du Endpoint Protection](../../../protect/deploy-use/monitor-endpoint-protection.md).  

### <a name="os-deployment"></a>Distribution av operativsystem

Mer information finns i [övervaka OS-distributioner](../../../osd/deploy-use/monitor-operating-system-deployments.md).

### <a name="monitor-power-management"></a>Övervaka energispar funktioner

Mer information finns i [övervaka och planera för energispar funktioner](../../clients/manage/power/monitor-and-plan-for-power-management.md).  

### <a name="monitor-software-metering"></a>Övervaka avläsning av program vara

Mer information finns i [övervaka app-användning med avläsning av program vara](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

### <a name="monitor-software-updates"></a>Övervaka programuppdateringar

Mer information finns i [övervaka program uppdateringar](../../../sum/deploy-use/monitor-software-updates.md).  


## <a name="monitor-the-site-hierarchy"></a><a name="BKMK_SH_Node"></a>Övervaka platshierarki

Noden **platshierarki på arbets** ytan **övervakning** ger en översikt över din Configuration Manager-hierarki och länkar mellan platser. Du kan använda två vyer:  

- **Hierarkidiagram**: visar hierarkin som en förenklad topologi som bara visar viktig information. Mer information finns i [Hierarkidiagram](#hierarchy-diagram).  

- **Geografisk vy**: visar dina platser på en geografisk karta som visar de plats platser som du konfigurerar. Mer information finns i [geografisk vy](#geographical-view).  

Använd noden **platshierarki om du vill** övervaka hälso tillståndet för varje plats. Övervaka även länkar mellan platser och deras relation till externa faktorer, t. ex. en geografisk plats.  

Både plats status och länkar mellan platser replikeras som plats data och inte globala data. När du ansluter Configuration Manager-konsolen till en underordnad primär plats kan du inte Visa plats-eller länk statusen för andra primära platser eller deras underordnade sekundära platser. I en hierarki med flera primära platser kan du till exempel visa statusen för underordnade sekundära platser, den primära platsen och den centrala administrations platsen när du ansluter-konsolen till en primär plats. I den här vyn kan du inte se status för andra platser under den centrala administrations webbplatsen.  

Om du vill kontrol lera visningen **i noden platshierarki** använder du åtgärden **Konfigurera inställningar** . Hierarkin replikerar de inställningar som du konfigurerar i den här noden.  

### <a name="hierarchy-diagram"></a>Hierarkidiagram

Hierarkidiagrammet visar upp platserna på en topologisk karta. Välj en plats och visa en sammanfattning av status meddelanden från den platsen. Gå igenom om du vill visa status meddelanden och få åtkomst till plats **egenskaperna**.  

Om du vill visa hög nivå status för en plats eller replikeringslänk mellan platser kan du Hovra mus pekaren över objektet. Status för replikeringslänk replikeras inte globalt. Om du vill visa information om replikeringslänken mellan alla primära platser i en hierarki ansluter du-konsolen till den centrala administrations platsen.  

Följande alternativ ändrar hierarkidiagrammet:  

#### <a name="groups"></a>Grupper

Konfigurera antalet primära platser och sekundära platser som utlöser en ändring i hierarki diagrammet. Den här ändringen i visningen kombinerar platserna till ett enda objekt. Sedan visas det totala antalet platser och en övergripande sammanställning av status meddelanden och plats status. Gruppkonfigurationer påverkar inte den geografiska vyn.  

#### <a name="favorite-sites"></a>Favorit platser

Ange att enskilda platser ska vara en favorit webbplats. En favoritplats markeras med en stjärnikon i hierarkidiagrammet. Favorit platser kombineras inte med andra platser när du använder grupper. De visas alltid individuellt.  

### <a name="geographical-view"></a>Geografisk vy

I den geografiska vyn visas varje plats på en geografisk karta. Den visar bara platser som du konfigurerar med en plats. När du väljer en plats i den här vyn visas länkar till överordnade eller underordnade platser. Till skillnad från vyn hierarki diagram kan du inte Visa information om plats status meddelande eller replikeringslänk i den här vyn.  

> [!NOTE]  
> Om du vill använda den geografiska vyn måste datorn som Configuration Manager-konsolen ansluter till ha Internet Explorer installerat och kunna komma åt Bing Maps via HTTP-protokollet.  

Följande alternativ ändrar den geografiska vyn:  

#### <a name="site-location"></a>Plats för webbplats

Ange en geografisk plats för varje plats med någon av följande typer:

- En gatuadress
- Ett plats namn som namnet på en stad
- Av latitud-och longitud-koordinater

Om du till exempel vill använda latitud och longitud för Redmond, Washington anger du **N 47 40 26,3572 W 122 7 17,4432** som plats för platsen. Du behöver inte ange symbolerna för grader, minuter eller sekunder för latitud eller longitud. Configuration Manager använder Bing Maps för att visa platsen i den geografiska vyn. Sedan kan du Visa din hierarki med de geografiska platserna. Den här vyn ger inblick i regionala problem som kan påverka specifika platser eller replikering mellan platser.  

När du anger en plats kan du söka efter en viss plats i hierarkin med hjälp av rutan **Plats**. Markera platsen och ange läget i form av ett ortnamn eller en gatuadress i kolumnen **Plats**. Configuration Manager använder Bing Maps för att lösa platsen.  

<a name="BKMK_MonitorRepLinksAndStatuss"></a>

## <a name="next-steps"></a>Nästa steg

[Övervaka databasreplikering](monitor-replication.md)
