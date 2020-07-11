---
title: Säkerhet och sekretess för kompatibilitetsinställningar
titleSuffix: Configuration Manager
description: Lär dig mer om rekommenderade säkerhets metoder för kompatibilitetsinställningar i Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 1c409244-6778-4970-a99c-d2508c9cf62b
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 5021a88966c6c57a3b49a907e14bbe06e28286ff
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240651"
---
# <a name="security-and-privacy-for-compliance-settings-in-configuration-manager"></a>Säkerhet och sekretess för kompatibilitetsinställningar i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*


## <a name="security-best-practices-for-compliance-settings"></a>Rekommenderade säkerhetsmetoder för kompatibilitetsinställningar  

|Regelverk för säkerhet|Mer information|  
|----------------------------|----------------------|  
|Övervaka inte känsliga data.|Undvik oönskad informationsspridning genom att inte konfigurera konfigurationsobjekt att övervaka potentiellt känslig information.|  
|Konfigurera inte kompatibilitetsregler som använder data som kan ändras av slutanvändare.|Om du skapar en kompatibilitetsregel baserat på data som användarna kan ändra, till exempel registerinställningar för konfigurationsalternativ, blir kompatibilitetsresultatet inte tillförlitligt.|  
|Importera bara konfigurationspaket för Microsoft System Center och andra konfigurationsdata från externa källor om de har en giltig digital signatur från en betrodd utgivare.|Publicerade konfigurationsdata kan signeras digitalt så att du kan kontrollera publiceringskällan och försäkra dig om att data inte har manipulerats. Om verifieringskontrollen av den digitala signaturen misslyckas varnas du och uppmanas att fortsätta med importen. Importera inte osignerade data om du inte kan verifiera datakällan och informationens integritet.|  
|Implementera åtkomstkontroller för att skydda referensdatorer|När en administrativ användare konfigurerar en register- eller filsysteminställning genom att navigera till en referensdator försäkrar du dig om att referensdatorn inte har komprometterats.|  
|Skydda kommunikationskanalen när du bläddrar till en referensdator.|För att förhindra manipulering av data när de överförs via nätverket använder du Internet Protocol security (IPsec) eller Server Message Block (SMB) mellan datorn som kör Configuration Manager-konsolen och referens datorn.|  
|Begränsa och övervaka administrativa användare som tilldelas den rollbaserade säkerhetsrollen Kompatibilitetsinställningshanteraren.|Administrativa användare som tilldelas rollen **Kompatibilitetsinställningshanteraren** kan distribuera konfigurationsobjekt till alla enheter och alla användare i hierarkin. Konfigurationsobjekt kan vara mycket kraftfulla och kan till exempel omfatta skript och registeromkonfigurationer.|  

## <a name="privacy-information-for-compliance-settings"></a>Sekretessinformation för kompatibilitetsinställningar  
 Du kan använda kompatibilitetsinställningar för att utvärdera om dina klientenheter är kompatibla med konfigurationsobjekt som du distribuerar i konfigurationsbaslinjer. Vissa inställningar kan justeras automatiskt om de inte är kompatibla. Kompatibilitetsinformation skickas till platsservern från hanteringsplatsen, och informationen lagras i platsdatabasen. Informationen krypteras när enheter skickar den till hanteringsplatsen men den lagras inte i krypterat format på platsdatabasen. Informationen sparas i databasen tills den raderas av platsunderhållsaktiviteten **Ta bort föråldrade data för Configuration Manager** , vilket sker var 90:e dag. Du kan konfigurera borttagningsintervallet. Information om kompatibilitet skickas inte till Microsoft.  

 Enheter utvärderar inte kompatibilitetsinställningar som standard. Dessutom måste du konfigurera konfigurationsobjekten och konfigurationsbaslinjerna och sedan distribuera dem till enheter.  
