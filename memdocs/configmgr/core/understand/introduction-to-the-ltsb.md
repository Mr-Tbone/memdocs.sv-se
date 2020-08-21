---
title: Introduktion till LTSB
titleSuffix: Configuration Manager
description: Lär dig mer om den långsiktiga etablerings grenen för Configuration Manager.
ms.date: 08/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 694bc29f-a7fd-4e06-815a-1a9c5e9ac563
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1370c1bf80283ff30ad54378ad58ecd9a5d24d47
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699372"
---
# <a name="introduction-to-the-long-term-servicing-branch-of-configuration-manager"></a>Introduktion till långsiktig service gren för Configuration Manager

*Gäller för: System Center Configuration Manager (långsiktig service gren)*

LTSB (Long-term Servicing Branch) för Configuration Manager är en distinkt gren som är utformad som ett installations alternativ som är tillgängligt för alla kunder. Men det är det enda alternativet för kunder som kan förfalla sin Software Assurance (SA) eller motsvarande prenumerations behörighet för Configuration Manager.

Baserat på Configuration Manager version 1606 har LTSB minskat funktioner jämfört med den aktuella grenen av Configuration Manager.

> [!TIP]   
> Configuration Manager-LTSB är inte relaterat till LTSC (System Center Suite Long term Servicing Channel). Mer information finns i [Översikt över versions alternativ för System Center](/system-center/ltsc-and-sac-overview).

## <a name="features-that-arent-available"></a>Funktioner som inte är tillgängliga

Den aktuella grenen av Configuration Manager stöder följande funktioner som inte är tillgängliga när du använder LTSB:

- Uppdateringar i konsolen som lägger till nya funktioner och förbättringar.
- Stöd för nyligen utgivna operativ system som ska användas som plats servrar och klienter.
- Lokal MDM
- Service instrument panel och service planer för Windows 10, inklusive stöd för de senaste versionerna av Windows 10.  
- Stöd för framtida versioner av Windows Server och Windows 10 LTSB
- Tillgångsinformation
- Molnbaserade distributionsplatser
- Exchange Online som en Exchange-anslutning    

Även om stöd för dessa funktioner inte är tillgängligt med LTSB, förblir vissa funktioner synliga i Configuration Manager-konsolen, men de kan inte väljas eller användas.

Moln integrering, samt funktioner som ingår i Configuration Manager nuvarande gren version 1610 eller senare, är inte tillgängliga för LTSB. Dessa funktioner omfattar, men är inte begränsade till följande:<!--SCCMDocs#1823-->

- Samhantering
- Desktop Analytics
- Gateway för molnhantering
- Azure Active Directory-integrering
- Appar från Microsoft Store för företag

## <a name="find-ltsb-documentation"></a>Hitta LTSB-dokumentation

LTSB baseras på den aktuella gren versionen 1606. Använd den [aktuella gren dokumentationen](../../index.yml), med varningar och begränsningar som är begränsade till LTSB. Dessa varningar och begränsningar identifieras i följande artiklar:

- [Installera LTSB](install-the-ltsb.md)
- [Uppgradera LTSB till aktuell gren](convert-to-current-branch.md)
- [Konfigurationer som stöds för LTSB](supported-configurations-for-ltsb.md)
- [Hantera LTSB för Configuration Manager](manage-the-ltsb.md)

När du refererar till den aktuella gren dokumentationen för LTSB gäller information som gäller för version 1606 eller tidigare även för LTSB. Funktioner eller information som introduceras med version 1610 eller senare stöds inte av LTSB.

## <a name="licensing-overview-for-the-ltsb"></a>Licens översikt för LTSB   

Kunder med aktiv Software Assurance (SA) på Configuration Manager licenser, eller med motsvarande prenumerations rättigheter från den 1 oktober 2016, har behörighet att använda den 2016 version 1606 som Configuration Manager. Kunder som har behörighet att Configuration Manager den 1 oktober 2016 hittar två licensierade alternativ vid installation: aktuell gren och långsiktig service gren (LTSB).

Kunder som har permanent rätt att System Center Configuration Manager, eller som tillåter SA eller prenumerationen att upphöra att vara efter 1 oktober, kan installera den version av System Center Configuration Manager LTSB som är aktuell vid tidpunkten för förfallet.

Mer information om de här licenserna finns i de [fullständiga villkoren för de produkter som du köper via Microsofts volym licensierings program](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?mode=1).

Mer information om licensiering för Configuration Manager grenar finns i [Configuration Manager licensiering och grenar](learn-more-editions.md).

## <a name="next-steps"></a>Nästa steg

Om du bestämmer att Configuration Manager LTSB är rätt gren för din miljö, installerar du [en ny LTSB](install-the-ltsb.md#install-a-new-site) -plats som en del av en ny hierarki eller [uppgraderar en System Center 2012-Configuration Manager plats](install-the-ltsb.md#upgrade-from-system-center-2012-configuration-manager) och hierarki.