---
title: Visningsprogrammet för mängdutvärdering
titleSuffix: Configuration Manager
description: Använd samlings utvärderings visaren för att visa och felsöka samlings utvärderings processen i Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: caad2d93-087c-4dc0-a2a7-6a2fd808b4c8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9ab75238e5dd26872847e68863ef603d3ac22671
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723420"
---
# <a name="collection-evaluation-viewer"></a>Visningsprogrammet för mängdutvärdering

*Gäller för: Configuration Manager (aktuell gren)*

Utvärderings versionen av samling är ett av de [Configuration Manager verktygen](tools.md). Använd den för att visa och felsöka samlings utvärderings processen på den primära plats servern.

Verktyget visar följande information:  

- Både historisk och Live-information för fullständiga och stegvisa samlings utvärderingar  

- Status för utvärderings kön  

- Tiden för att samlings utvärderingar ska slutföras  

- Vilka samlingar som för närvarande utvärderas  

- Beräknad tid som en samlings utvärdering startar och slutförs  



## <a name="about-collection-evaluation"></a>Om samlings utvärdering

Utvärderings processen för samlingen körs genom att utvärdera medlemskaps reglerna för en samling för att uppdatera dess medlemmar. Platsen placerar en samling som den utvärderas i någon av fyra olika köer:  

- **Manuell kö**: för samlingar som en administratör har valt att utvärdera manuellt från konsolen  

- **Ny kö**: för nyligen skapade samlingar  

- **Fullständig kö**: för samlingar som är klara för fullständig utvärdering  

- **Stegvis kö**: för samlingar med stegvis utvärdering  

Det finns fyra trådar som körs för att utvärdera samlingarna i ovanstående köer. Varje kö innehåller en serie matriser, och varje matris innehåller de samlingar som ska utvärderas. Den tråd som körs för kön väljer en samling från matrisen och kör utvärderingen. Längden på kön anger antalet matriser i kön.



## <a name="requirements"></a>Krav

- Kör verktyget på plats servern  

- Kör verktyget av en administrativ användare med minst den **skrivskyddade analytiker** rollen  

- Användaren måste också ha behörigheten **läsa** till plats databasen i SQL



## <a name="usage"></a>Användning

Kör **CEViewer. exe**. Verktygets huvud meny innehåller följande flikar: 

- [Anslut](#bkmk_connect): etablera den första anslutningen till den primära plats servern och SQL Server  

- [Fullständig utvärdering](#bkmk_full-eval): visar detaljerad information om alla tidigare fullständiga utvärderingar   

- [Stegvis utvärdering](#bkmk_incremental-eval): visar detaljerad information om alla tidigare stegvisa utvärderingar  

- [Alla köer](#bkmk_all-q): sammanfattar de aktuella samlings utvärderingarna för alla fyra köer  

- [Manuell kö](#bkmk_manual-q): visar detaljerad information om den aktuella samlings utvärderingen i den manuella kön  

- [Ny kö](#bkmk_new-q): visar detaljerad information om den aktuella samlings utvärderingen i den nya kön  

- [Fullständig kö](#bkmk_full-q): visar detaljerad information om den aktuella samlings utvärderingen i hela kön  

- [Stegvis kö](#bkmk_incremental-q): visar detaljerad information om den aktuella samlings utvärderingen i den stegvisa kön  


### <a name="connect-tab"></a><a name="bkmk_connect"></a>Fliken Anslut

På den här fliken kan du upprätta den första anslutningen till den primära plats servern. Verktyget upprättar också en anslutning till den SQL Server som är värd för plats databasen.

Anslutningarna till både den primära plats servern och SQL-servrarna använder den aktuella inloggade användarens autentiseringsuppgifter. Anslutningar till den centrala administrations platsen eller en sekundär plats stöds inte. Ingen samlings utvärderings process körs på dessa platser.

När verktyget har upprättat en anslutning, se ett meddelande längst ned i utvärderings versionen av samlingen som bekräftar verktygets anslutning till SQL-servern. 


### <a name="full-evaluation-tab"></a><a name="bkmk_full-eval"></a>Fliken fullständig utvärdering

Visar detaljerad information om de tidigare utvärderingarna av fullständig samling. Det finns åtta kolumner:  

- **Samlings namn**: samlingens namn  

- **Webbplats-ID**: plats-ID för samlingen   

- **Kör tid**: hur länge den sista samlings utvärderingen kördes, i sekunder  

- **Senaste avslutnings tid för utvärdering**: när den sista samlings utvärderingen har slutförts  

- **Nästa utvärderings tid**: när nästa fullständiga utvärdering börjar  

- **Medlems ändringar**: medlemmens ändringar i den sista samlings utvärderingen. Dessa ändringar är antingen plus (medlemmar tillagda) eller minus (borttagna medlemmar).  

- **Senaste ändrings tid för medlems**: den senaste gången som medlemskapet ändrades i samlings utvärderingen  

- **Procent**: procent andelen utvärderings tid för den här samlingen över den totala utvärderings tiden för alla samlingar  


### <a name="incremental-evaluation-tab"></a><a name="bkmk_incremental-eval"></a>Fliken stegvis utvärdering

Visar detaljerad information om utvärderingar av tidigare stegvisa samlingar. Det finns sju kolumner:  

- **Samlings namn**: samlingens namn  

- **Webbplats-ID**: plats-ID för samlingen   

- **Kör tid**: hur länge den sista samlings utvärderingen kördes, i sekunder  

- **Senaste avslutnings tid för utvärdering**: när den sista samlings utvärderingen har slutförts  

- **Medlems ändringar**: medlemmens ändringar i den sista samlings utvärderingen. Dessa ändringar är antingen plus (medlemmar tillagda) eller minus (borttagna medlemmar).  

- **Senaste ändrings tid för medlems**: den senaste gången som medlemskapet ändrades i samlings utvärderingen  

- **Procent**: procent andelen utvärderings tid för den här samlingen över den totala utvärderings tiden för alla samlingar  


### <a name="all-queues-tab"></a><a name="bkmk_all-q"></a>Fliken alla köer

Sammanfattar Live Collection-utvärderingar för alla fyra köer. Det finns sex avsnitt:  

- **Sammanfattning**: visar det totala samlings numret och köns längd för alla samlingar i alla fyra köer  

- **Kör utvärdering**: visar vilken samling som för närvarande utvärderas i varje kö och hur länge den har körts  

- **Manuell uppdatering**: visar en kort sammanfattning av de samlingar som utvärderas, den uppskattade slut tiden och ordningen på utvärderingen i den manuella kön  

- **Ny samling**: visar en kort sammanfattning av de samlingar som utvärderas, den uppskattade slut tiden och utvärderings ordningen i den nya samlings kön  

- **Fullständig utvärdering**: visar en kort sammanfattning av de samlingar som utvärderas, den uppskattade slut tiden och utvärderings ordningen i den fullständiga utvärderings kön  

- **Stegvis utvärdering**: visar en kort sammanfattning av de samlingar som utvärderas, den uppskattade slut tiden och utvärderings ordningen i den stegvisa utvärderings kön  


### <a name="manual-queue-tab"></a><a name="bkmk_manual-q"></a>Fliken manuell kö

Visar information om den manuella samlings utvärderingen som utvärderas för närvarande. Ordningen i listan är den ordning i vilken samlingen kommer att utvärderas. Det finns fyra kolumner:  

- **Samlings namn**: samlingens namn  

- **Webbplats-ID**: plats-ID för samlingen   

- **Beräknad slut för ande tid**: När utvärderingen beräknas att slutföras  

- **Beräknad körnings tid**: hur länge utvärderingen ska köras, på dag: timme: minut: andra format  


### <a name="new-queue-tab"></a><a name="bkmk_new-q"></a>Fliken Ny kö

Visar live-information om den nya samlings utvärderingen som utvärderas. Ordningen i listan är den ordning i vilken samlingen kommer att utvärderas. Det finns fyra kolumner:  

- **Samlings namn**: samlingens namn  

- **Webbplats-ID**: plats-ID för samlingen   

- **Beräknad slut för ande tid**: När utvärderingen beräknas att slutföras  

- **Beräknad körnings tid**: hur länge utvärderingen ska köras, på dag: timme: minut: andra format  


### <a name="full-queue-tab"></a><a name="bkmk_full-q"></a>Flik för fullständig kö

Visar information om den fullständiga samlings utvärderingen som för närvarande utvärderas. Ordningen i listan är den ordning i vilken samlingen kommer att utvärderas. Det finns fyra kolumner:  

- **Samlings namn**: samlingens namn  

- **Webbplats-ID**: plats-ID för samlingen   

- **Beräknad slut för ande tid**: När utvärderingen beräknas att slutföras  

- **Beräknad körnings tid**: hur länge utvärderingen ska köras, på dag: timme: minut: andra format  


### <a name="incremental-queue-tab"></a><a name="bkmk_incremental-q"></a>Fliken stegvis kö

Visar information om den stegvisa samlings utvärderingen som utvärderas för närvarande. Ordningen i listan är den ordning i vilken samlingen kommer att utvärderas. Det finns fyra kolumner:  

- **Samlings namn**: samlingens namn  

- **Webbplats-ID**: plats-ID för samlingen   

- **Beräknad slut för ande tid**: När utvärderingen beräknas att slutföras  

- **Beräknad körnings tid**: hur länge utvärderingen ska köras, på dag: timme: minut: andra format  



