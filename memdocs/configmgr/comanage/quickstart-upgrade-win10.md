---
title: Uppgradera Windows 10
titleSuffix: Configuration Manager
description: Uppgradera enheter till Windows 10 version 1709 eller senare, vilket krävs för samtidig hantering
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 561eb5b6-f90c-485a-91c2-e45bb0ce7877
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e11a6130fb9f7d86b7d3377cc4120d4e61c43d2d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711464"
---
# <a name="upgrade-windows-10-for-co-management"></a>Uppgradera Windows 10 för samhantering

När du arbetar för att registrera din organisation för samhantering, är det viktigt att bli en betydande Hurdle för vissa kunder. Co-Management kräver [Windows 10 version 1709](https://docs.microsoft.com/windows/whats-new/whats-new-windows-10-version-1709) eller senare. När du uppdaterar Windows och konfigurerar automatisk registrering registreras dina klienter automatiskt för samhantering.

I följande videoklipp är Senior program hanterare Anders York och produkt marknadsförings hanterarens låsnings-Ainley diskutera och demo som uppgraderar till Windows 10 för samhantering:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Upgrading-to-Windows-10-to-Enable-Co-Management/player]



## <a name="why-upgrade"></a>Varför uppgradera?

Bland andra plattforms framsteg, Windows 10 version 1709 och senare har stöd för automatisk registrering. Det här beteendet gör att en enhet registreras automatiskt i Intune när den anslöts Azure Active Directory (Azure AD). 

Mer information finns i [Aktivera automatisk registrering i Windows 10](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment).


## <a name="how-to-do-it"></a>Gör så här

Här följer några tips som vi har lärt oss från att hjälpa flera tusentals kunder att komma igång snabbt:

- Använd stegvisa distributioner för att distribuera uppgraderingen till rätt personer vid rätt tidpunkt. Mer information finns i skapa stegvisa [distributioner](../osd/deploy-use/create-phased-deployment-for-task-sequence.md).  

- Använd för cachelagring för att minska vänte tiden för användare. Mer information finns i [Konfigurera förinställt innehåll för cache](../osd/deploy-use/configure-precache-content.md).  

- Använd standard mal len för att uppgradera en aktivitetssekvens på plats. Konfigurera sedan stegen för för-och efter-uppgradering, samt eventuella problem åtgärder. Mer information finns i [rekommenderade steg i aktivitetssekvensen för efter bearbetning](../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#recommended-task-sequence-steps-for-post-processing).  

- Om din miljö har en mycket mobil personal styrka, Configuration Manager stöder uppgradering på plats via Cloud Management Gateway (CMG). Med den här funktionen kan du uppgradera Windows 10-klienter när de är Internet-baserade. Mer information om CMG finns i [distribuera Windows 10 på plats-uppgradering via CMG](../osd/deploy-use/deploy-a-task-sequence.md#deploy-windows-10-in-place-upgrade-via-cmg).  

- Erbjud en deltagande för samhantering för användare som vill vara tidiga medarbetare. Den här metoden påskyndar det första införandet. Genom att identifiera dessa personer i förväg kan du se till att du har en lämplig täckning under de första dagarna i distributionen. Du får också validering och feedback från användare som är glada över förändringar och intresserade av mer frekventa versioner. Tidiga antagandeprogram genererar nya tekniker och ökar i storlek över tid.  


## <a name="case-studies"></a>Fallstudier

Microsoft IT distribuerade Windows 10 till 96 000-distribuerade användare på Microsoft. I distributionen ingår både fjärran vändare och användare i företags nätverket. Distributionen slutfördes inom nio veckor. Mer information om deras erfarenhet finns i [distribuera Windows 10 på Microsoft som en uppgradering på plats](https://www.microsoft.com/itshowcase/deploying-windows-10-at-microsoft-as-an-in-place-upgrade).  

En stor europeisk program varu tillverkare har använt en tidig antagande grupp. Efter den första testningen och pilot gruppen får cirka 2 000 anställda den första uppdateringen, uppgraderingar och program vara. I den här gruppen ingår IT-personal och deltagande i frivilliga. Den här nivån av engagemang med sina användare ger dem högre tillförlitlighet vid testning och mer trovärdighet när Mass distributioner börjar.



## <a name="contact-fasttrack"></a>Kontakta FastTrack

Om du behöver hjälp med uppgraderingen av Windows 10 när som helst i processen går du till [Microsoft FastTrack](https://Microsoft.com/FastTrack/), loggar in och ber om hjälp. 

Mer information finns i [få hjälp från FastTrack](quickstart-fasttrack.md). 

