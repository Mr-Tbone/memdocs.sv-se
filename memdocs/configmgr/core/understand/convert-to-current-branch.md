---
title: Uppgradera LTSB till aktuell gren
titleSuffix: Configuration Manager
description: Lär dig hur du konverterar en LTSB-plats (långsiktig Servicing Branch) till en aktuell förgrenings plats.
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ec5b54cf-62b7-4ed1-9bb3-e8c63b9641c8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b9f79eae1eee29fee33a9a841a303aae55686c55
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722958"
---
# <a name="upgrade-the-long-term-servicing-branch-to-the-current-branch"></a>Uppgradera den långsiktiga service grenen till den aktuella grenen

*Gäller för: System Center Configuration Manager (långsiktig service gren)*

Använd det här avsnittet om du vill lära dig att uppgradera (konvertera) en plats och hierarki som kör LTSB (Long-term Servicing Branch) för Configuration Manager till Current Branch.

När du har ett aktuellt Software Assurance-avtal (eller liknande licens rättigheter) som ger dig behörighet att använda Current Branch, kan du konvertera installationen från LTSB till Current Branch.  Detta är en enkelriktad konvertering eftersom det inte finns stöd för att konvertera en Current Branch-plats till LTSB.

Om du har flera platser behöver du bara konvertera platsen på den översta nivån i hierarkin. När platsen på den översta nivån har konverterats:
- Underordnade primära platser konverteras automatiskt.
- Du måste manuellt uppdatera sekundära platser i Configuration Manager-konsolen.

## <a name="run-setup-to-convert-the-long-term-servicing-branch"></a>Kör installations programmet för att konvertera långsiktig service gren
På platsen på den översta nivån i hierarkin kan du köra Configuration Manager-installationen från kvalificerande bas linje medium och välja **plats underhåll**.  När du sedan visas på sidan licensiering väljer du alternativet för Current Branch och Slutför guiden.

När platsen har konverterats till Current Branch, kommer tidigare funktioner och funktioner som inte är tillgängliga att användas.

> [!NOTE]  
> Kvalificerande bas linje medium är ett medium som har en version som är lika med eller senare än din LTSB-installation.

Eftersom LTSB baseras på version 1606 kan du till exempel inte använda bas linjen 1511 media för att konvertera till Current Branch. I stället kör du installationen från samma version 1606-bas linje medium som du använde för att installera LTSB-platsen och väljer alternativet licensiering för Current Branch.  Alternativt, om en senare bas linje för Current Branch har frigjorts, kan du köra installationen från det bas linje mediet.

En lista över bas linje versioner finns i **bas linje-och uppdaterings versioner** i [uppdateringar för Configuration Manager](../servers/manage/updates.md).

## <a name="use-the-configuration-manager-console-to-convert-the-long-term-servicing-branch"></a>Använd Configuration Manager-konsolen för att konvertera långsiktig service gren
Om din webbplats kör LTSB kan du använda följande alternativ i Configuration Manager-konsolen för att konvertera till Current Branch:

 1. I-konsolen går du till **Administration** > **plats konfiguration** > **platser**och öppnar sedan **Inställningar för hierarkin**.  

 2. Växla till fliken **licensiering** i **Inställningar för hierarki**. Välj alternativet att **konvertera till Current Branch**och välj sedan **Använd**.  

När platsen har konverterats till Current Branch, kommer tidigare funktioner och funktioner som inte är tillgängliga att användas.
