---
title: Uppgradera Linux- och UNIX-klienter
titleSuffix: Configuration Manager
description: Uppgradera en klient på en Linux-eller UNIX-server i Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7d2bb377-1005-4a55-bd1f-b80a6d0b22e1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f71a36dff92f888d595538ff2fd483d7c212358f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715398"
---
# <a name="how-to-upgrade-clients-for-linux-and-unix-servers-in-configuration-manager"></a>Uppgradera klienter för Linux-och UNIX-servrar i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

> [!Important]  
> Från och med version 1902 stöder Configuration Manager inte Linux-eller UNIX-klienter. 
> 
> Överväg Microsoft Azure hantering för hantering av Linux-servrar. Azure-lösningar har omfattande Linux-support som i de flesta fall överskrider Configuration Manager-funktioner, inklusive slut punkt till slut punkt för korrigerings hantering för Linux.

Du kan uppgradera versionen av klienten för Linux och UNIX på en dator till en nyare klientversion utan att först avinstallera den befintliga klienten. Det gör du genom att installera det nya klient installations paketet på datorn när du använder kommando rads egenskapen **-keepdb** . När klienten för Linux och UNIX installeras skrivs befintliga klientdata över med de nya klientfilerna. Kommando rads egenskapen **-keepdb** styr dock installations processen för att behålla klientens unika IDENTIFIERARE (GUID), lokal informations databas och certifikat arkiv. Den här informationen används sedan av den nya klientinstallationen.  

 Anta till exempel att du har en RHEL5 x64-dator där klienten körs från den ursprungliga versionen av Configuration Manager-klienten för Linux och UNIX. Om du vill uppgradera den här klienten till klient versionen från Cumulative Update 1 kör du **installations** skriptet manuellt för att installera tillämpligt klient paket från kumulativ uppdatering 1, med tillägg av kommando rads växeln **-keepdb** . Se följande exempel kommando rad:  

`./install -mp <hostname\> -sitecode <code\> -keepdb ccm-Universal-x64.<build\>.tar`  



## <a name="how-to-use-a-software-deployment-to-upgrade-the-client-on-linux-and-unix-servers"></a>Uppgradera klienten på Linux- och UNIX-servrar med hjälp av en programdistribution  
 Du kan använda en programdistribution för att uppgradera klienten för Linux och UNIX till en ny klientversion. Configuration Manager klienten kan dock inte köra installations skriptet direkt för att installera den nya klienten eftersom installationen av en ny klient först måste avinstallera den aktuella klienten. Med den här åtgärden avslutas den Configuration Manager klient process som kör installations skriptet innan installationen av den nya klienten börjar. För att kunna använda en program distribution för att installera den nya klienten måste du schemalägga installationen så att den startar vid ett senare tillfälle och körs av operativ systemets inbyggda schemaläggnings funktioner.  

 Använd en program distribution för att först kopiera filerna för det nya klient installations paketet till klient datorn. Sedan distribuerar du och kör ett skript för att schemalägga klient installations processen. Skriptet använder operativ systemets inbyggda **at** -kommando för att fördröja starten. När skriptet körs, hanteras åtgärden av klient operativ systemet och inte Configuration Manager-klienten på datorn. På så sätt kan kommando raden som anropas av skriptet först avinstallera Configuration Manager-klienten och sedan installera den nya klienten. De här åtgärderna Slutför uppgraderingen av klienten på Linux-eller UNIX-datorn. När uppgraderingen är klar hanteras den uppgraderade klienten fortfarande av Configuration Manager.  

 Följ stegen nedan om du vill konfigurera en programdistribution som uppgraderar klienten för Linux och UNIX. Följande steg och exempel uppgraderar en RHEL5 x64-dator som kör den ursprungliga versionen av klienten till klientversionen Cumulative Update 1.  

#### <a name="to-use-a-software-deployment-to-upgrade-the-client-on-linux-and-unix-servers"></a>Så här uppgraderar du klienten på Linux- och UNIX-servrar med hjälp av en programdistribution  

1. Kopiera det nya klient installations paketet till datorn som kör Configuration Manager-klienten för att uppgradera.  

    Du kan till exempel placera klient installations paketet och installera skript för Cumulative Update 1 på följande plats på klient datorn: **/tmp/patch**  

2. Skapa ett skript för att hantera uppgraderingen av Configuration Manager-klienten. Placera sedan en kopia av skriptet i samma mapp på klient datorn som klientens installationsfiler från steg 1.  

    Skriptet kräver inte något angivet namn. Det måste innehålla kommando rader som är tillräckliga för att använda klientens installationsfiler från en lokal mapp på klient datorn och för att installera klient installations paketet med hjälp av kommando rads egenskapen **-keepdb** . Använd kommando rads egenskapen **-keepdb** för att underhålla den unika identifieraren för den aktuella klienten för användning av den nya klienten som du installerar.  

    Skapa till exempel ett skript med namnet **Upgrade.sh** som innehåller följande rader:  

   ```  
   #!/bin/sh  
   #  
   /tmp/PATCH/install -sitecode <code> -mp <hostname> -keepdb /tmp/PATCH/ccm-Universal-x64.<build>.tar  

   ```  

    Kopiera den sedan till mappen **/tmp/patch** på klient datorn.

3. Använd en programdistribution om du vill att klienterna ska använda datorns inbyggda **at** -kommando för att köra skriptet **upgrade.sh** med en kort fördröjning innan det körs.  

    Använd till exempel följande kommando rad för att köra skriptet: **at-f/tmp/Upgrade.sh-m nu + 5 minuter**  

   När klienten har schemalagt körningen av **upgrade.sh** -skriptet skickar den ett statusmeddelande som anger att programdistributionen har slutförts. Dock hanteras själva klientinstallationen sedan av datorn, efter fördröjningen. När klientuppgraderingen har slutförts verifierar du installationen genom att granska filen **/var/opt/microsoft/scxcm.log** på klientdatorn. Bekräfta att klienten är installerad och kommunicerar med platsen genom att visa information om klienten i noden **enheter** i arbets ytan **till gångar och efterlevnad** i Configuration Manager-konsolen.  
