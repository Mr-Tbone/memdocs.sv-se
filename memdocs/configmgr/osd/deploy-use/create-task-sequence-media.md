---
title: Skapa aktivitetssekvensmedia
titleSuffix: Configuration Manager
description: Skapa medier för aktivitetssekvenser för att distribuera ett operativ system till en måldator i din Configuration Managers miljö.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 90498b4b-6a9b-43cd-b465-1d6c9a52df1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 87d5df6edee2adba32f1a49b8e867e930386b4df
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711030"
---
# <a name="create-task-sequence-media"></a>Skapa aktivitetssekvensmedia

*Gäller för: Configuration Manager (aktuell gren)*

Du kan använda Media för att avbilda en operativ system avbildning från en referens dator eller för att distribuera ett operativ system till en måldator i din Configuration Managers miljö. De media som du skapar kan vara CD, DVD eller en USB-flash-enhet.  

Media används främst för att distribuera operativ system på mål datorer som inte har en nätverks anslutning eller som har en anslutning med låg bandbredd till din Configuration Manager-plats. Du kan dock också använda Media för att starta en OS-distribution utanför ett befintligt Windows-operativsystem. Den här metoden är användbar när det inte finns något befintligt operativ system, operativ systemet inte fungerar eller om du vill partitionera om hård disken.  

Distributionsmedia omfattar startbara media, fristående media och förberedda media. Innehållet i mediet varierar beroende på vilken typ av media du använder. Till exempel innehåller fristående media den aktivitetssekvens som distribuerar operativ systemet. Andra typer av media hämtar aktivitetssekvenser från hanterings platsen.  

> [!IMPORTANT]  
> Du måste vara administratör på datorn där du kör Configuration Manager-konsolen för att skapa media för aktivitetssekvenser. Om du inte är administratör uppmanas du att ange administratörsautentiseringsuppgifter när du startar guiden skapa aktivitetssekvens.  


## <a name="capture-media"></a><a name="BKMK_PlanCaptureMedia"></a>Avbilda Media

Med avbildnings medier kan du avbilda en operativ system avbildning från en referens dator. Avbildnings medier innehåller den Start avbildning som startar referens datorn och den aktivitetssekvens som avbildar operativ system avbildningen.

Mer information om hur du skapar avbildnings medier finns i [skapa avbildnings medier](create-capture-media.md).  


## <a name="bootable-media"></a><a name="BKMK_PlanBootableMedia"></a>Startbara media

Startbara medier innehåller följande komponenter:

- Start avbildningen
- Valfria för [inläsnings kommandon](../understand/prestart-commands-for-task-sequence-media.md) och deras nödvändiga filer
- Configuration Manager binärfiler

När mål datorn startar ansluter den till nätverket och hämtar aktivitetssekvensen, operativ system avbildningen och eventuellt annat nödvändigt innehåll från nätverket. Eftersom aktivitetssekvensen inte finns på mediet kan du ändra aktivitetssekvensen eller innehållet utan att behöva återskapa mediet.  

> [!IMPORTANT]  
> Paketen på startbara medier är inte krypterade. Vidta lämpliga säkerhets åtgärder, till exempel att lägga till ett lösen ord till mediet, för att se till att paket innehållet skyddas från obehöriga användare.  

Mer information om hur du skapar startbara medier finns i [Skapa startbara media](create-bootable-media.md).  


## <a name="prestaged-media"></a><a name="BKMK_PlanPrestagedMedia"></a>För berett medium

Med för beredda medier kan du använda startbara medier och en operativ system avbildning på en hård disk före etablerings processen. Det förinstallerade mediet är en WIM-fil (Windows Image). Den kan installeras på en dator utan operativ system av tillverkaren eller i mellanlagrings centret som inte är ansluten till produktions Configuration Managers miljön.  

För beredda medier innehåller den Start avbildning som används för att starta mål datorn och den OS-avbildning som används på mål datorn. Du kan även ange program, paket och drivrutinspaket som ska ingå som en del av de förinstallerade medierna. Den aktivitetssekvens som distribuerar operativ systemet ingår inte i mediet. När du distribuerar en aktivitetssekvens som använder för beredda medier kontrollerar klienten om det finns giltigt innehåll i den lokala aktivitetssekvensen. Om innehållet inte hittas eller har ändrats laddar klienten ned innehållet från en distributions plats eller en peer.  

Förberedda medier tillämpas på hårddisken på en ny dator innan datorn skickas till slutanvändaren. När datorn startas första gången efter att du har tillämpat det förinstallerade mediet startar datorn i Windows PE. Den ansluter till en hanterings plats för att hitta aktivitetssekvensen som slutför distributions processen för operativ systemet.  

> [!IMPORTANT]  
> Paketen på för beredda medier är inte krypterade. Vidta lämpliga säkerhets åtgärder, till exempel att lägga till ett lösen ord till mediet, för att se till att paket innehållet skyddas från obehöriga användare.  

Mer information om hur du skapar för beredda medier finns i [Skapa förinstallerade medier](create-prestaged-media.md).  


## <a name="stand-alone-media"></a><a name="BKMK_PlanStandaloneMedia"></a>Fristående media

Fristående media innehåller allt som krävs för att distribuera operativ systemet. Det här innehållet omfattar aktivitetssekvensen och eventuellt annat nödvändigt innehåll. Eftersom allt som krävs för att distribuera operativ systemet lagras på fristående media är disk utrymmet som krävs för fristående media större än för andra typer av medier.  

Mer information om hur du skapar fristående medier finns i [skapa fristående media](create-stand-alone-media.md).  


## <a name="considerations-when-using-https"></a>Att tänka på när du använder HTTPS

När du konfigurerar hanterings platser och distributions platser för att använda HTTPS, skapar du startmedia och för beredda medier på en primär plats, inte den centrala administrations platsen. Tänk också på följande plats för att hjälpa dig att avgöra om du ska konfigurera mediet som dynamiska eller platsbaserade:  

- Om du vill konfigurera mediet som dynamiska medier måste alla primära platser ha rot certifikat utfärdaren (CA) för den plats som du skapade mediet från. Du kan importera rotcertifikatutfärdaren till alla primära platser i hierarkin.  

- När primära platser i din Configuration Manager-hierarki använder olika rot certifikat utfärdare måste du använda platsbaserade medier på varje plats.  
