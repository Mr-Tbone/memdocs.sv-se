---
title: Översikt över anslutna CMPivot-innehavare
titleSuffix: Configuration Manager
description: Översikt över CMPivot för Microsoft Endpoint Manager-klient anslutna enheter.
ms.date: 08/17/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: 31bf1359-54e5-4416-9f39-6bb0070db542
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 529cf0c27793262abb2902477ceab11201212b1e
ms.sourcegitcommit: 62b451396eae660f2d5289ae3666b19ed1cc666d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/19/2020
ms.locfileid: "88614718"
---
# <a name="tenant-attach-cmpivot-overview"></a>Klient anslutning: CMPivot-översikt

*Gäller för: Configuration Manager (Technical Preview Branch)*

> [!Important]
> Den här artikeln gäller för den tekniska för hands versionen av Configuration Manager. Mer information finns i [Configuration Manager Technical Preview version 2005](../core/get-started/2020/technical-preview-2005.md#bkmk_cmpivot).

Med CMPivot kan du snabbt bedöma status för en enhet i din miljö och vidta åtgärder. När du anger en fråga kommer CMPivot att köra en fråga i real tid på den aktuella anslutna enheten. De data som returneras kan sedan filtreras, grupperas och finjusteras för att besvara affärs frågor, felsöka problem i din miljö eller reagera på säkerhetshot. Mer information om hur du använder CMPivot finns i [använda CMPivot](../core/servers/manage/cmpivot.md).

## <a name="refine-cmpivot-queries"></a><a name="bkmk_refine"></a> Förfina CMPivot-frågor

När du använder CMPivot från administratörs konsolen för Microsoft Endpoint Manager ser du till att dina frågor är justerade för prestanda. Om du begär en fråga med en data uppsättning som är för stor kan du få `Error: The query result is too large, retry with additional filters` . Förfina frågan så att den blir mer detaljerad om du ser det här felet. Följande operatorer används ofta för att förfina frågor:

- Använd `count` om du bara behöver returnerat antal objekt.
- Använd `project` om du bara behöver vissa kolumner.
- Används `take` för att returnera upp till det angivna antalet rader.
- Används `top` för att returnera de första N posterna sorterade efter angivna kolumner.

> [!Important]
> När du använder CMPivot för att fråga en enhet, och om det inte finns något svar inom 10 minuter, kommer frågan att vara tids gräns. <!--7802754-->


[!INCLUDE [Overview article sections for both Microsoft Endpoint Manager and Configuration Manager use](../core/servers/manage/includes/cmpivot-overview-shared.md)]


## <a name="next-steps"></a>Nästa steg

Fler exempel skript finns i [Microsoft Endpoint Manager-klient anslutning: CMPivot-skript exempel](cmpivot-samples-attached.md).
