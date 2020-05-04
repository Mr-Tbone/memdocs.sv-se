---
title: Plats system roller för klienter
titleSuffix: Configuration Manager
description: Bestäm plats system roller för klienter i Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 984e8d92-7327-4b08-9228-0c955e6ac778
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 32895df466c41ca828d1107857212b8d5a777026
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713249"
---
# <a name="determine-the-site-system-roles-for-configuration-manager-clients"></a>Fastställa plats system roller för Configuration Manager klienter

*Gäller för: Configuration Manager (aktuell gren)*

Den här artikeln kan hjälpa dig att bestämma vilka plats system roller du behöver för att distribuera Configuration Manager klienter.

Mer information om var de här rollerna ska installeras i hierarkin finns i [utforma en hierarki med platser](../../../plan-design/hierarchy/design-a-hierarchy-of-sites.md).  

Mer information om hur du installerar och konfigurerar dessa roller finns i [Installera plats system roller](../../../servers/deploy/configure/install-site-system-roles.md).  

## <a name="management-point"></a>Hanteringsplats

Som standard använder alla Windows-klientdatorer en distributions plats för att installera Configuration Manager-klienten. De kan återgå till en hanterings plats när en distributions plats inte är tillgänglig. Du kan dock installera Windows-klienter på datorer från en alternativ källa när du använder kommando rads egenskapen `/source:<Path>`CCMSetup. Du kan till exempel utföra den här åtgärden om du installerar klienter på Internet. Ett annat scenario är om du vill undvika att skicka nätverks paket mellan datorn och hanterings platsen under klient installationen. Det här scenariot beror på att en brand vägg blockerar de begärda portarna eller eftersom du har en anslutning med låg bandbredd. Alla klienter måste dock kommunicera med en hanterings plats för att kunna tilldelas en-plats och hanteras av Configuration Manager.  

Mer information om klientens kommando rads egenskaper finns i [om klient installations egenskaper](../about-client-installation-properties.md).  

När du installerar fler än en hanterings plats i-hierarkin ansluter klienterna automatiskt till en punkt baserat på deras skogs medlemskap och nätverks plats. Du kan inte installera fler än en hanterings plats på en sekundär plats.  

Mac-klientdatorer och klienter för mobila enheter som du registrerar med Configuration Manager kräver alltid en hanterings plats för klient installation. Den här hanterings platsen måste finnas på en primär plats, måste vara konfigurerad för att stödja mobila enheter och måste acceptera klient anslutningar från Internet. De här klienterna kan inte använda hanterings platser på sekundära platser eller ansluta till hanterings platser på andra primära platser.  

## <a name="distribution-point"></a>Distributionsplats

Du behöver ingen distributions plats för att installera Configuration Manager-klienter på Windows-datorer. Som standard använder Configuration Manager en distributions plats för att installera klientens källfiler på Windows-datorer. Det kan gå tillbaka till att ladda ned dessa filer från en hanterings plats. Distributions platser används inte för att installera mobila enhets klienter som har registrerats med Configuration Manager, men används om du installerar den äldre klienten för mobila enheter. Om du installerar Configuration Manager-klienten som en del av en operativ system distribution, lagras OS-avbildningen och hämtas från en distributions plats.

Även om du kanske inte behöver distributions platser för att installera de flesta Configuration Manager-klienter, behöver du dem för att installera program vara som program och program varu uppdateringar på klienterna.  

## <a name="fallback-status-point"></a>Status för återställningsplats

Du kan använda en återställnings status punkt för att övervaka klient distribution för Windows-datorer. Du kan också identifiera de Windows-klientdatorer som är ohanterade eftersom de inte kan kommunicera med en hanterings plats.

Följande klient typer använder inte en återställnings status punkt:

- Mac-datorer
- Mobila enheter som har registrerats av Configuration Manager
- Mobila enheter som hanteras med Exchange Server-anslutningen

Ingen återställnings status punkt krävs för att övervaka klient aktivitet och klient hälsa.  

Återställnings status punkten kommunicerar alltid med klienter via HTTP, som använder oautentiserade anslutningar och skickar data i klartext. Det här beteendet gör återställnings status punkten sårbar för angrepp, särskilt när den används med Internetbaserad klient hantering. För att minska angrepps ytan ska du alltid dedikera en server för att köra återställnings status punkten. Installera inte andra plats system roller på samma server i en produktions miljö.  

Installera en återställnings status punkt om samtliga följande villkor gäller:  

- Du vill att klient kommunikations fel från Windows-datorer ska skickas till platsen, även om dessa klient datorer inte kan kommunicera med en hanterings plats.  

- Du vill använda Configuration Manager klient distributions rapporter som visar de data som skickas av återställnings status platsen.  

- Du har en dedikerad server för den här plats system rollen och har ytterligare säkerhets åtgärder för att skydda servern mot angrepp.  

- Fördelarna med att använda en återställnings status punkt uppväger eventuella säkerhets risker kopplade till oautentiserade anslutningar och klar text överföringar över HTTP-trafik.  

Installera inte en återställnings status punkt om säkerhets riskerna för att köra en webbplats med oautentiserade anslutningar och rensade text överföringar uppväger fördelarna med att identifiera klient kommunikations problem.  

## <a name="reporting-services-point"></a>Rapporteringstjänstpunkt

Configuration Manager innehåller många rapporter som hjälper dig att övervaka installationen, tilldelningen och hanteringen av klienter i Configuration Manager-konsolen. Några av klient distributions rapporterna kräver att klienterna tilldelas en återställnings status plats.  

Rapporterna behövs inte för att distribuera klienter. Du kan se viss distributions information i Configuration Manager-konsolen eller använda klientens loggfiler för detaljerad information. Klient rapporterna ger dock värdefull information som hjälper dig att övervaka och felsöka klient distribution.  

## <a name="enrollment-point-and-enrollment-proxy-point"></a>Registreringsplats och registreringsproxyplats

Configuration Manager kräver registrerings platsen och registrerings platsen för proxy för att registrera mobila enheter och registrera certifikat för Mac-datorer. Du behöver inte dessa plats system roller i följande situationer:

- Du planerar att hantera mobila enheter med Exchange Server-anslutningen
- Du installerar den äldre klienten för mobila enheter, till exempel för Windows CE
- Du begär och installerar klient certifikatet på Mac-datorer oberoende av Configuration Manager

## <a name="application-catalog"></a>Program katalog

> [!Important]  
> Program katalogens Silverlight-användar upplevelse stöds inte av den aktuella gren versionen 1806. Från och med version 1906 använder uppdaterade klienter automatiskt hanterings platsen för program distributioner som är tillgängliga för användare. Du kan inte heller installera nya program katalog roller. Support upphör för program katalog rollerna med version 1910.  
>
> Mer information finns i följande artiklar:
>
> - [Konfigurera Software Center](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Borttagna och föråldrad funktioner](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

## <a name="cloud-management-gateway-connector-point"></a>Cloud Management Gateway-kopplings punkt

Du behöver en Cloud Management Gateway-kopplings punkt om du konfigurerar en [moln hanterings-Gateway](../../manage/cmg/plan-cloud-management-gateway.md) för att [Hantera klienter på Internet](../../manage/manage-clients-internet.md).
