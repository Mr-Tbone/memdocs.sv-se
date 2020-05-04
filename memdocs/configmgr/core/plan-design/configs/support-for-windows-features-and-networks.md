---
title: Stöd för Windows-funktioner
titleSuffix: Configuration Manager
description: Lär dig vilka Windows-och nätverksfunktioner som Configuration Manager stöder.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0cf4bacb-6b6d-4d4f-8640-b13fe15873de
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7e8e65571a3902661176ca3840690c159faef416
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709623"
---
# <a name="support-for-windows-features-and-networks-in-configuration-manager"></a>Stöd för Windows-funktioner och nätverk i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Den här artikeln beskriver Configuration Manager stöd för vanliga funktioner i Windows och nätverksfunktioner.  

## <a name="branchcache"></a><a name="bkmk_branchcache"></a>BranchCache  

Använd Windows BranchCache med Configuration Manager när du aktiverar den på distributions platser och konfigurera klienterna så att de använder den i läget för distribuerad cache.

Konfigurera BranchCache-inställningarna för en distributions typ för program, för en paket distribution och för aktivitetssekvenser. Från och med version 1802 är BranchCache aktiverat som standard.

När kraven för BranchCache är uppfyllda, aktiverar den här funktionen klienter på fjärrplatser för att hämta innehåll från lokala klienter som har en aktuell cache för innehållet.  

Till exempel när den första BranchCache-aktiverade klienten begär innehåll från en distributions plats som har kon figurer ATS som en BranchCache-server, laddar klienten ned och cachelagrar innehållet. Det här innehållet görs sedan tillgängligt för klienter i samma undernät som begärde det här innehållet.

Dessa klienter cachelagrar också innehållet. Andra klienter i samma undernät behöver inte hämta innehåll från distributions platsen. Innehållet distribueras över flera klienter för framtida överföringar.  

### <a name="requirements-to-support-branchcache-with-configuration-manager"></a>Krav som stöd för BranchCache med Configuration Manager

#### <a name="configure-distribution-points"></a>Konfigurera distributions platser

Lägg till **Windows BranchCache** -funktionen på den plats system server som har kon figurer ATS som en distributions plats.

- Distributions platser på servrar som har kon figurer ATS för att stödja BranchCache kräver ingen ytterligare konfiguration.
- Du kan inte lägga till Windows BranchCache till en molnbaserad distributions plats. Molnbaserade distributions platser stöder nedladdning av innehåll via klienter som har kon figurer ATS för Windows BranchCache.  

#### <a name="configure-clients"></a>Konfigurera klienter

- Klienter som har stöd för BranchCache måste konfigureras för BranchCache-läget för distribuerad cache.  
- OS-inställningen för BITS-klientinställningar måste aktive ras för att stöda BranchCache.  

Mer information finns i [Konfigurera klienter för BranchCache](https://docs.microsoft.com/windows/deployment/update/waas-branchcache#configure-clients-for-branchcache) i Windows-dokumentationen.

Alla Configuration Manager-versioner som stöds av Windows stöder BranchCache som standard.

Mer information finns i [BranchCache för Windows](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) i Windows Server-dokumentationen.  

## <a name="computers-in-workgroups"></a><a name="bkmk_Workgroups"></a>Datorer i arbets grupper  

Configuration Manager ger stöd för klienter i arbets grupper.  

- Configuration Manager stöder flytt av en klient från en arbets grupp till en domän eller från en domän till en arbets grupp. Mer information finns i [så här installerar du Configuration Manager-klienter på arbets grupps datorer](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientWorkgroup).  

> [!NOTE]
> Även om klienter i arbets grupper stöds måste alla plats system vara medlemmar i en Active Directory-domän som stöds.  

## <a name="data-deduplication"></a><a name="bkmmk_datadedup"></a>Datadeduplicering

Configuration Manager stöder användning av datadeduplicering med distributions platser på Windows Server 2012 eller senare.

> [!IMPORTANT]  
> Volymen som är värd för paketets källfiler kan inte markeras för datadeduplicering. Den här begränsningen beror på att datadeduplicering använder referens punkter. Configuration Manager stöder inte användning av en innehålls käll plats med filer som lagras på referens punkter.  

Mer information finns i följande inlägg:

- [Configuration Manager distributions platser och Windows Server 2012-datadeduplicering](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configuration-manager-distribution-points-and-windows-server/ba-p/273385) på Configuration Manager teamets blogg

- [Översikt över datadeduplicering](https://docs.microsoft.com/windows-server/storage/data-deduplication/overview) i Windows Server-dokumentationen

## <a name="directaccess"></a><a name="bkmk_DA"></a>DirectAccess  

Configuration Manager stöder DirectAccess-funktionen för kommunikation mellan klienter och plats server system.  

- När alla krav för DirectAccess är uppfyllda kan Configuration Manager-klienter på Internet kommunicera med sin tilldelade plats som om de befann sig i intranätet.  

- För åtgärder som initieras av servern, t. ex. fjärr styrning och push-installation av klienter, måste den initierande datorn köra IPv6. Det här protokollet måste stödjas på alla mellanliggande nätverks enheter.  

Configuration Manager stöder inte följande funktioner i DirectAccess:  

- Distribution av operativsystem

- Kommunikation mellan Configuration Manager-platser  

- Kommunikation mellan Configuration Manager plats system servrar inom en plats  

## <a name="dual-boot-computers"></a><a name="bkmk_dualboot"></a>Datorer med flervalsstart  

Configuration Manager kan inte hantera mer än ett operativ system på samma dator. Om det finns fler än ett operativ system på en dator som ska hanteras justerar du platsens identifierings-och klient installations metoder för att säkerställa att Configuration Manager-klienten endast installeras på det operativ system som måste hanteras.  

## <a name="ipv6"></a><a name="bkmk_IPv6"></a>IPv6  

Utöver Internet Protocol version 4 (IPv4) stöder Configuration Manager Internet Protocol version 6 (IPv6), med följande undantag:  

|Funktion| Undantag till IPv6-stöd|  
|--------------|-------------------------------|  
|Molnbaserade distributionsplatser|IPv4 krävs för Microsoft Azure och molnbaserade distributionsplatser.|  
|Gateway för molnhantering|IPv4 krävs för att stödja Microsoft Azure och Cloud Management Gateway.|  
|Mobila enheter som har registrerats av Microsoft Intune och Microsoft Service Connector|IPv4 krävs för att stödja mobila enheter som har registrerats av Microsoft Intune och Microsoft Service Connector.|  
|Nätverksidentifiering|IPv4 krävs om du konfigurerar en DHCP-server för sökning i Nätverksidentifiering.|  
|Distribution av operativsystem|I version 1802 och tidigare krävs IPv4 för att stödja OS-distribution.  </br> </br> Från och med version 1806 aktiverar du en PXE-svarare på en distributions plats utan Windows Deployment-tjänst. Den här nya PXE responder-tjänsten stöder IPv6. Andra aspekter av funktionen för distribution av operativ system, till exempel att hämta eller ange statiska IP-adresser under aktivitetssekvensen, fortsätter att kräva IPv4. |  
|Kommunikation med aktiveringsproxy|IPv4 krävs för klientens aktiveringsproxypaket.|  
|Windows CE|IPv4 krävs för att stödja Configuration Manager-klienten på Windows CE enheter.|  

## <a name="network-address-translation"></a><a name="bkmk_NAT"></a>Översättning av nätverks adresser  

NAT (Network Address Translation) stöds inte i Configuration Manager, om inte platsen stöder klienter som finns på Internet och klienten identifierar att den är ansluten till Internet. Mer information om Internetbaserad klient hantering finns i [Planera för att hantera Internetbaserade klienter](../../clients/manage/plan-internet-based-client-management.md).  

## <a name="specialized-storage-technology"></a><a name="bkmk_storage"></a>Specialiserad lagrings teknik  

Configuration Manager fungerar med all maskin vara som är certifierad i listan Windows-maskinvarukompatibilitet för den version av operativ systemet som Configuration Manager-komponenten är installerad på.

Plats Server roller kräver NTFS, så att Configuration Manager kan ange katalog-och fil behörigheter. Configuration Manager förutsätter att den har fullständig ägande rätt till en logisk enhet. Plats system som körs på separata datorer kan inte dela en logisk partition på någon lagrings teknik. Varje dator kan dock använda en separat logisk partition på samma fysiska partition på en delad lagringsenhet.  

### <a name="support-considerations"></a>Support överväganden

- San ( **Storage Area**Network): ett SAN-nätverk (Storage Area Network) stöds när en Windows-baserad server som stöds är direkt ansluten till den volym som hanteras av San-nätverket.  

- **Single Instance Storage**: Configuration Manager stöder inte konfiguration av distributions plats paket och signaturinställningar på en SIS-aktiverad volym (Single Instance Storage).  

     Dessutom stöds inte cache för en Configuration Manager-klient på en SIS-aktiverad volym.  

- **Flyttbar disk enhet**: Configuration Manager stöder inte installation av Configuration Manager plats system eller klienter på en flyttbar disk enhet.  
