---
title: UNIX/Linux klient komponent tjänster och kommandon
titleSuffix: Configuration Manager
description: Lär dig mer om komponent tjänster och kommandon på Linux-och UNIX-klienter i Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e5a8c79f-5791-49c5-8055-086d742e5559
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: de564595ce51a336b5f11d4050928fa812269601
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713347"
---
# <a name="linux-and-unix-clients-component-services-and-commands-for-configuration-manager"></a>Linux-och UNIX-klienter komponent tjänster och kommandon för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

> [!Important]  
> Från och med version 1902 stöder Configuration Manager inte Linux-eller UNIX-klienter. 
> 
> Överväg Microsoft Azure hantering för hantering av Linux-servrar. Azure-lösningar har omfattande Linux-support som i de flesta fall överskrider Configuration Manager-funktioner, inklusive slut punkt till slut punkt för korrigerings hantering för Linux.


 I följande tabell visas klient komponent tjänsterna i Configuration Manager-klienten för Linux och UNIX.  

|Filnamn|Mer information|  
|---------------|----------------------|  
|ccmexec.bin|Den här tjänsten liknar ccmexc-tjänsten på en Windows-baserad klient. Den ansvarar för all kommunikation med Configuration Manager plats system roller och kommunicerar även med tjänsten omiserver. bin för att samla in maskin varu inventering från den lokala datorn.<br /><br /> En lista över kommando rads argument som stöds får köras`ccmexec -h`|  
|omiserver.bin|Den här tjänsten är CIM-servern. CIM-servern innehåller ett ramverk för anslutningsbara programvarumoduler som kallas providrar. Providrar interagerar med Linux och UNIX-datorresurser och samlar in maskinvaruinventeringsdata. **Processprovidern** för en Linux-dator samlar till exempel in data som är kopplad till Linux-operativsystemprocesserna.|  

 Följande tabeller anger kommandon som du kan använda för att starta, stoppa eller starta om klienttjänsterna (ccmexec.bin och omiserver.bin) på varje version av Linux eller UNIX. När du startar eller stoppar tjänsten ccmexec startas och stoppas även tjänsten omiserver.  

|Operativsystem|Kommandon|  
|----------------------|--------------|  
|Universal Agent<br /><br /> RHEL 4 och SLES 9|Har`/etc/init d/ccmexecd start`<br /><br /> Stanna:`/etc/init d/ccmexecd stop`<br /><br /> Börja`/etc/init d/ccmexecd restart`|  
|Solaris 9|Har`/etc/init d/ccmexecd start`<br /><br /> Stanna:`/etc/init d/ccmexecd stop`<br /><br /> Börja`/etc/init d/ccmexecd restart`|  
|Solaris 10|Start:<br /><br /> `svcadm enable -s svc:/application/management/omiserver`<br /><br /> `svcadm enable -s svc:/application/management/ccmexecd`<br /><br /> Stopp:<br /><br /> `svcadm disable -s svc:/application/management/ccmexecd`<br /><br /> `svcadm disable -s svc:/application/management/omiserver`|  
|Solaris 11|Start:<br /><br /> `svcadm enable -s svc:/application/management/omiserver`<br /><br /> `svcadm enable -s svc:/application/management/ccmexecd`<br /><br /> Stopp:<br /><br /> `svcadm disable -s svc:/application/management/ccmexecd`<br /><br /> `svcadm disable -s svc:/application/management/omiserver`|  
|AIX|Start:<br /><br /> `startsrc -s omiserver`<br /><br /> `startsrc -s ccmexec`<br /><br /> Stopp:<br /><br /> `stopsrc -s ccmexec`<br /><br /> `stopsrc -s omiserver`|  
|HP-UX|Har`/sbin/init.d/ccmexecd start`<br /><br /> Stanna:`/sbin/init.d/ccmexecd stop`<br /><br /> Börja`/sbin/init.d/ccmexecd restart`|  
