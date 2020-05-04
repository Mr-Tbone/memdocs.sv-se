---
title: Samverkan mellan versioner
titleSuffix: Configuration Manager
description: Lär dig hur du undviker konflikter mellan flera Configuration Manager hierarkier i samma nätverk.
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9b0a7859-747f-4495-a2f4-13fd5991f897
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d8d5eeeeafa775514bb46fa0906f22572343611d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713088"
---
# <a name="interoperability-between-different-versions-of-configuration-manager"></a>Samverkan mellan olika versioner av Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Du kan installera och använda flera, oberoende hierarkier av Configuration Manager i samma nätverk. Men eftersom olika hierarkier av Configuration Manager inte interagerar utanför migreringsprocessen, kräver varje hierarki konfigurationer för att förhindra konflikter mellan dem. Dessutom kan du skapa vissa konfigurationer för att hjälpa resurser som du hanterar interagerar med plats systemen från rätt hierarki.  

## <a name="interoperability-between-current-branch-and-earlier-versions"></a><a name="BKMK_SupConfigInterop"></a>Interoperabilitet mellan aktuell gren och tidigare versioner  

Platser med olika versioner kan inte finnas i samma Configuration Manager-hierarki. De enda undantagen är under processen för följande uppgraderings scenarier:

- Från System Center 2012 Configuration Manager till Configuration Manager aktuella grenen
- Från en Configuration Manager aktuella gren versionen till en nyare version med hjälp av konsol uppdateringar

Du kan distribuera en Configuration Manager aktuella gren platsen och hierarkin sida vid sida med en befintlig System Center 2012-Configuration Manager webbplats eller hierarki. Planera för att förhindra att klienter från någon version försöker ansluta till en plats från den andra versionen.

Om exempelvis två eller fler Configuration Manager hierarkier har [överlappande gränser](../../servers/deploy/configure/boundary-groups.md#overlapping-boundaries) som omfattar samma nätverks platser, tilldelar du varje ny klient till en speciell plats i stället för att använda automatisk platstilldelning. Mer information finns i [tilldela klienter till en plats](../../clients/deploy/assign-clients-to-a-site.md).  

Dessutom kan du inte installera en-klient från System Center 2012 Configuration Manager på en dator som är värd för en plats system roll från Configuration Manager aktuella grenen. Du kan inte heller installera en Configuration Manager aktuella gren klienten på en dator som är värd för en plats system roll från System Center 2012 Configuration Manager.  

Följande klienter och anslutningar stöds inte:  

- Alla System Center 2012 Configuration Manager eller tidigare dator klient version  

- Alla System Center 2012 Configuration Manager eller en tidigare enhets hanterings klient  

- Windows CE Platform Builder enhets hanterings klient (alla versioner)  

- System Center Mobile Device Manager, VPN-anslutning  

### <a name="client-site-assignment-considerations"></a><a name="BKMK_SupConfigSiteAssignment"></a> Att tänka på vid tilldelningen av klienter till platser  

Configuration Manager klienter kan bara tilldelas till en enda primär plats. Det går inte att förutsäga den faktiska platstilldelning för en klient om samtliga följande villkor är uppfyllda:

- Du använder automatisk platstilldelning för att tilldela klienter till en plats under klient installationen
- Mer än en avgränsnings grupp innehåller samma gränser
- Gränserna grupper har olika tilldelade platser

Om gränserna överlappar över flera Configuration Manager platser och hierarkier, kanske inte klienterna tilldelas till den plats som du förväntar dig, eller så kanske den inte tilldelas till en webbplats alls.  

Configuration Manager aktuella gren klienter kontrollerar platsens version innan den slutför platstilldelning. Om plats gränser överlappar varandra kan du inte tilldela klienter till en plats med en tidigare version. Tidigare System Center 2012 Configuration Manager-klienter kan dock felaktigt tilldelas till en senare Configuration Manager aktuella gren platsen.  

För att förhindra att klienter oavsiktligt tilldelas till fel plats när två hierarkier har överlappande gränser, konfigurerar du parametrarna för klient installation för att tilldela klienter till en speciell plats.  

## <a name="configuration-manager-limitations-in-a-mixed-version-hierarchy"></a><a name="bkmk_mixed"></a>Configuration Manager begränsningar i en hierarki med blandade versioner  

När du uppgraderar en Configuration Manager aktuell Branch-hierarki finns det tillfällen då olika platser har olika versioner. Till exempel måste du först uppgradera den centrala administrations platsen. På grund av plats underhålls fönster uppgraderar du inte de primära platserna förrän efter ett senare tillfälle och datum.  

Om olika platser i samma hierarki kör olika versioner är vissa funktioner inte tillgängliga. Det här beteendet kan påverka hur du hanterar Configuration Manager objekt i Configuration Manager-konsolen och vilka funktioner som är tillgängliga för klienter. Normalt är funktioner från den nya versionen av Configuration Manager inte tillgängliga på platser eller till klienter som kör en lägre service pack version.  

### <a name="network-access-account"></a>Nätverksåtkomstkonto

Du uppgraderar den centrala administrations platsen till Configuration Manager aktuella grenen. Du kan visa konto informationen för nätverks åtkomst från en Configuration Manager-konsol som är ansluten till den här uppdaterade platsen. Det visar inte konto information från platser som fortfarande kör System Center 2012 Configuration Manager.

När du har uppgraderat den primära platsen till samma version som den centrala administrations platsen visas konto informationen i-konsolen.

Samma sak gäller när du uppdaterar mellan versioner av Configuration Manager.

### <a name="boot-images-for-os-deployment"></a>Start avbildningar för distribution av operativ system

#### <a name="when-upgrading-from-system-center-2012-configuration-manager-to-configuration-manager-current-branch"></a>När du uppgraderar från System Center 2012 Configuration Manager till Configuration Manager aktuella grenen

När platsen på den översta nivån i en hierarki uppgraderas till Configuration Manager aktuella grenen, uppdaterar den automatiskt standard start avbildningarna för att använda Windows Assessment and Deployment Kit (ADK) version 10. Använd dessa start avbildningar endast för distributioner till klienter på Configuration Manager aktuella gren platser. Mer information finns i [Planera för interoperabilitet med OS-distribution](../../../osd/plan-design/planning-for-operating-system-deployment-interoperability.md).

#### <a name="when-upgrading-between-configuration-manager-current-branch-versions"></a>När du uppgraderar mellan Configuration Manager aktuella gren versioner

Så länge nya versioner av Configuration Manager inte uppdaterar den version av Windows ADK som används, finns det ingen inverkan på Start avbildningarna.

### <a name="new-task-sequence-steps"></a>Nya uppgiftssekvenssteg

När du skapar en aktivitetssekvens med ett steg som introducerats i en version av Configuration Manager som inte är tillgänglig i en tidigare version, kan följande problem uppstå:

- Ett fel inträffar när du försöker redigera aktivitetssekvensen från en plats som kör en tidigare version av Configuration Manager.

- Aktivitetssekvensen körs inte på en dator som kör en tidigare version av Configuration Manager-klienten.

### <a name="client-to-down-level-management-point-communications"></a>Kommunikation mellan klienter och äldre hanterings platser

En Configuration Manager-klient som kommunicerar med en hanterings plats från en plats som kör en lägre version än klienten kan endast använda funktioner som stöds av den äldre versionen av Configuration Manager. Om du till exempel distribuerar innehåll från en Configuration Manager aktuella gren plats som nyligen har uppgraderats till en klient som kommunicerar med en hanterings plats som ännu inte har uppgraderats till den versionen, kan den klienten inte använda nya funktioner från den senaste versionen.

### <a name="package-and-task-sequence-deployments-to-legacy-clients"></a>Distributioner av paket och aktivitetssekvensdistributioner till äldre klienter

<!-- SCCMDocs-pr issue #3493 -->

Från och med version 1902 kan du inte distribuera ett paket eller en aktivitetssekvens till en klient version 5,7730 eller tidigare. Undvik den här begränsningen genom att uppgradera klienten till en senare version.

## <a name="software-updates"></a>Programuppdateringar

### <a name="orchestration-groups"></a>Orkestreringsgrupper

Orchestration-grupper, som introducerades i version 2002, kan inte användas i en hierarki med blandade versioner. <!--SCCMDocs-pr issue ##5056, 6389000-->

## <a name="interoperability-for-the-configuration-manager-console"></a><a name="BKMK_ConsoleInterop"></a>Interoperabilitet för Configuration Manager-konsolen  

Det här avsnittet innehåller information om hur du använder Configuration Manager-konsolen i en miljö som har en blandning av Configuration Manager-versioner.  

### <a name="an-environment-with-both-system-center-2012-configuration-manager-and-configuration-manager-current-branch"></a>En miljö med både System Center 2012 Configuration Manager och Configuration Manager aktuell gren

För att kunna hantera en Configuration Manager-plats måste både konsolen och den plats konsolen ansluts till köra samma version av Configuration Manager. Du kan till exempel inte använda en System Center 2012-Configuration Manager-konsol för att hantera en Configuration Manager nuvarande gren plats eller på annat sätt runt.

Det finns inte stöd för att installera både System Center 2012-Configuration Manager-konsolen och den Configuration Manager aktuella gren konsolen på samma dator.

### <a name="an-environment-with-multiple-versions-of-configuration-manager"></a>En miljö med flera versioner av Configuration Manager

Configuration Manager aktuella grenen stöder inte installation av mer än en enda Configuration Manager-konsol på en dator. Om du vill använda flera konsoler som är särskilda för olika versioner av Configuration Manager installerar du de olika konsolerna på olika datorer.

Under uppdaterings processen för platser i en hierarki till en ny version kan du ansluta en konsol till en plats som kör en senare version och Visa information om andra platser i den hierarkin. Den här konfigurationen rekommenderas dock inte. Det är möjligt att skillnader mellan konsol versionen och Configuration Manager plats version kan leda till data problem. Vissa funktioner som är tillgängliga i den senaste produkt versionen är inte tillgängliga i-konsolen.

Det finns inte stöd för att hantera en-plats när du använder en-konsol med en version som inte matchar plats versionen. Om du gör det kan det leda till förlust av data och kan utgöra en risk för din webbplats. Det finns till exempel inte stöd för att använda en-konsol från version 1610 för att hantera en plats som kör version 1606.
