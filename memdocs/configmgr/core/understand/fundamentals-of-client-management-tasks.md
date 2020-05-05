---
title: Grundläggande om klient hantering
titleSuffix: Configuration Manager
description: Lär dig mer om aktiviteter som du kör för att hantera Configuration Manager-klienter.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8d4e5641-354e-4439-8b4f-620a760e233d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d58a0da25d98089a54694a21d47d1ef8583acb81
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722867"
---
# <a name="fundamentals-of-client-management-tasks-for-configuration-manager"></a>Grunderna i klient hanterings aktiviteter för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

När du har installerat Configuration Manager-klienter finns det flera uppgifter som du kör för att hantera klienterna.  Några av uppgifterna körs från Configuration Manager-konsolen. Andra aktiviteter körs från Configuration Manager klient programmet. Configuration Manager klient programmet installeras med Configuration Manager klient program varan.

## <a name="configuration-manager-console-tasks"></a>Configuration Manager konsol uppgifter
 I Configuration Manager-konsolen kan du utföra olika klient hanterings aktiviteter:  

-   Distribuera program, programuppdateringar, underhållsskript och operativsystem. Konfigurera installationen för ett visst datum och en angiven tidpunkt, gör program varan tillgänglig för användare att installera när de begär det, eller konfigurera program som ska avinstalleras.  

-   Skydda datorer mot skadlig kod och säkerhetshot samt få meddelanden när problem identifieras.  

-   Definiera de klient konfigurations inställningar som du vill övervaka och åtgärda om de inte är kompatibla.  

-   Samla in inventeringsinformation om maskin- och programvara, bland annat övervakning och avstämning av licensinformation från Microsoft.  

-   Felsöka datorer med fjärrstyrning.  

-   Implementera energisparinställningar för att hantera och övervaka datorernas energiförbrukning.  

Configuration Manager-konsolen övervakar tidigare aktiviteter i nära real tid. Meddelande-och statusinformation för varje aktivitet är tillgängligt i Configuration Manager-konsolen. Använd de integrerade rapporterings funktionerna i SQL Server Reporting Services om du vill samla in data och historiska trender. Klienter skickar information till platsen som klientstatus.  Klient statusinformation tillhandahåller data om hälso tillståndet för klienten och klient aktiviteten och visas i-konsolen eller med hjälp av de inbyggda rapporterna för Configuration Manager. Dessa data hjälper till att identifiera datorer som inte svarar och i vissa fall åtgärdas problem automatiskt.  

 Mer information om hanterings aktiviteter för klienter finns i [Hantera klienter](../../core/clients/manage/manage-clients.md) och [Hantera klienter för Linux-och UNIX-servrar](../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md). Läs om hur du använder rapporter i   
            [Introduktion till rapportering](../../core/servers/manage/introduction-to-reporting.md).  

## <a name="configuration-manager-client-application"></a>Configuration Manager klient program  
 När du installerar Configuration Manager-klientprogramvaran installeras även Configuration Manager klient programmet. Till skillnad från Software Center har Configuration Manager klient programmet utformats för supportavdelningen snarare än för slutanvändaren. Vissa konfigurations alternativ kräver lokal administratörs behörighet och de flesta alternativ kräver teknisk kunskap om hur Configuration Manager klient programmet fungerar. Med det här programmet kan du utföra följande uppgifter för en klient:  

-   Visa egenskaper för klienten, till exempel versions nummer, dess tilldelade plats, hanterings platsen den kommunicerar med och om klienten använder ett PKI-certifikat (Public Key Infrastructure) eller ett självsignerat certifikat.  

-   Bekräfta att klienten har laddat ned en klient princip efter att klienten har installerats för första gången. Bekräfta också att klient inställningarna är aktiverade eller inaktiverade som förväntat, enligt de klient inställningar som har kon figurer ATS i Configuration Manager-konsolen.  

-   Starta klient åtgärder. Du kan till exempel Ladda ned klient principen om en ny konfigurations ändring har utförts i Configuration Manager-konsolen och du inte vill vänta till nästa schemalagda tid.  

-   Tilldela en-klient till en Configuration Manager-plats manuellt eller försök hitta en plats. Ange sedan den Domain Name System (DNS)-suffixet för hanterings platser som publicerar till DNS.  

-   Konfigurera klientens cacheminne som temporärt lagrar filer. Ta sedan bort filer i cachen om du behöver mer disk utrymme för att installera program vara.  

-   Konfigurera inställningar för internetbaserad klienthantering.  

-   Visa konfigurationsbaslinjer som har distribuerats till klienten, starta kompatibilitetsutvärdering och visa kompatibilitetsrapporter.  
