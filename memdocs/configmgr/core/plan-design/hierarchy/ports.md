---
title: Portar som används för anslutningar
titleSuffix: Configuration Manager
description: Läs om de nödvändiga och anpassningsbara nätverks portarna som Configuration Manager använder för anslutningar.
ms.date: 04/29/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c6777fb0-0754-4abf-8a1b-7639d23e9391
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2495c0d7b5b19b5d6f7741d3b28b6a9a0e213fc3
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700154"
---
# <a name="ports-used-in-configuration-manager"></a>Portar som används i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Den här artikeln innehåller de nätverks portar som Configuration Manager använder. Vissa anslutningar använder portar som inte kan konfigureras och vissa stöder anpassade portar som du anger. Om du använder någon port filtrerings teknik kontrollerar du att de nödvändiga portarna är tillgängliga. Dessa port filtrerings tekniker omfattar brand väggar, routrar, proxyservrar eller IPsec.

> [!NOTE]  
> Om du stöder Internetbaserade klienter genom att använda SSL-bryggning, förutom port krav, kan du också behöva tillåta vissa HTTP-verb och-huvuden att passera brand väggen.

## <a name="ports-you-can-configure"></a><a name="BKMK_ConfigurablePorts"></a> Portar som du kan konfigurera

Med Configuration Manager kan du konfigurera portarna för följande typer av kommunikation:  

- Programkatalog webbplats till Programkatalog webb tjänst punkt  

- Proxy för registreringsplats till registreringsplats  

- Klient-till-plats-system som kör IIS  

- Klient till Internet (som proxyserverinställningar)  

- Program uppdaterings plats till Internet (som proxyserverinställningar)  

- Programuppdateringsplats till WSUS-server  

- Platsserver till platsdatabasserver  

- Plats Server till WSUS-databasserver

- Reporting Services-platser  

  > [!NOTE]  
  > Portarna som används för repor ting Services-platsens plats system roll konfigureras i SQL Server Reporting Services. Dessa portar används sedan av Configuration Manager under kommunikation till repor ting Services-platsen. Se till att granska dessa portar som definierar IP-filter-information för IPsec-principer eller för att konfigurera brand väggar.  

Som standard är HTTP-porten som används för kommunikation mellan klienter och plats port 80 och standard-HTTPS-porten är 443. Portar för kommunikation mellan klient och plats system via HTTP eller HTTPS kan ändras under installationen eller i plats egenskaperna för din Configuration Manager plats.  

Portarna som används för repor ting Services-platsens plats system roll konfigureras i SQL Server Reporting Services. Dessa portar används sedan av Configuration Manager under kommunikation till repor ting Services-platsen. Se till att granska dessa portar när du definierar IP-filter-information för IPsec-principer eller för att konfigurera brand väggar.  

## <a name="non-configurable-ports"></a><a name="BKMK_NonConfigurablePorts"></a> Portar som inte går att konfigurera  

Configuration Manager låter dig inte konfigurera portar för följande typer av kommunikation:  

- Plats till plats  

- Platsserver till platssystem  

- Configuration Manager-konsol till SMS-provider  

- Configuration Manager-konsolen till Internet  

- Anslutningar till moln tjänster, till exempel Microsoft Intune och moln distributions platser  

## <a name="ports-used-by-configuration-manager-clients-and-site-systems"></a><a name="BKMK_CommunicationPorts"></a> Portar som används av Configuration Manager-klienter och-plats system  

Följande avsnitt innehåller information om vilka portar som används för kommunikation i Configuration Manager. Pilarna i avsnitts rubriken visar riktningen för kommunikationen:  

- --> indikerar att en dator startar kommunikationen och att den andra datorn alltid svarar  

- &lt;--> indikerar att en dator kan starta kommunikation  

### <a name="asset-intelligence-synchronization-point----microsoft"></a><a name="BKMK_PortsAI"></a> Tillgångsinformation plats för synkronisering--> Microsoft  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

### <a name="asset-intelligence-synchronization-point----sql-server"></a><a name="BKMK_PortsAI-to-SQL"></a> Tillgångsinformation plats för synkronisering--> SQL Server  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|SQL över TCP|--|1433 <sup> [Anmärkning 2](#bkmk_note2) alternativ port tillgänglig</sup>|  

### <a name="application-catalog-web-service-point----sql-server"></a><a name="BKMK_PortsAppCatalogService-SQL"></a> Programkatalog-webb tjänst punkt--> SQL Server  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|SQL över TCP|--|1433 <sup> [Anmärkning 2](#bkmk_note2) alternativ port tillgänglig</sup>|  

### <a name="application-catalog-website-point----application-catalog-web-service-point"></a><a name="BKMK_PortsAppCatalogWebSitePoint_AppCatalogWebServicePoint"></a> Programkatalog webbplats--> Programkatalog webb tjänst punkt  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup> [Anmärkning 2](#bkmk_note2) alternativ port tillgänglig</sup>|  
|HTTPS|--|443 <sup> [Anmärkning 2](#bkmk_note2) alternativ port tillgänglig</sup>|  

### <a name="client----application-catalog-website-point"></a><a name="BKMK_PortsClient-AppCatalogWebsitePoint"></a> Klient--> Programkatalog webbplats  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup> [Anmärkning 2](#bkmk_note2) alternativ port tillgänglig</sup>|  
|HTTPS|--|443 <sup> [Anmärkning 2](#bkmk_note2) alternativ port tillgänglig</sup>|  

### <a name="client----client"></a><a name="BKMK_PortsClient-ClientWakeUp"></a> Klient--> klient  

Wake-up proxy använder också ICMP Echo Request-meddelanden från en klient till en annan klient. Klienter använder den här kommunikationen för att bekräfta om den andra klienten är aktiv i nätverket. ICMP kallas ibland ping-kommandon. ICMP har inte ett UDP-eller TCP-protokollnummer, så det visas inte i tabellen nedan. Men alla värdbaserade brandväggar på dessa klientdatorer eller mellanliggande nätverksenheter inom undernätet måste tillåta ICMP-trafik om aktiveringsproxykommunikationen ska fungera.  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|Wake on LAN|9 <sup> [Anmärkning 2](#bkmk_note2) alternativ port tillgänglig</sup>|--|  
|Aktiveringsproxy|25536 <sup> [Anmärkning 2](#bkmk_note2) alternativ port tillgänglig</sup>|--|  
|Windows PE peer-cache-sändning|8004|--|  
|Hämtning av peer-cache i Windows PE|--|8003|  

Mer information finns i [peer-cache i Windows PE](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md#BKMK_PeerCacheRequirements).

### <a name="client----configuration-manager-network-device-enrollment-service-ndes-policy-module"></a><a name="BKMK_PortsClient-PolicyModule"></a> Klient--> Configuration Manager princip module för registrerings tjänsten för nätverks enheter (NDES)

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP||80|  
|HTTPS|--|443|  

### <a name="client----cloud-distribution-point"></a><a name="BKMK_PortsClient-CloudDP"></a> Klient--> moln distributions plats  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

Mer information finns i [portar och data flöde](use-a-cloud-based-distribution-point.md#bkmk_dataflow).

### <a name="client----cloud-management-gateway-cmg"></a><a name="bkmk_client-cmg"></a> Klient – > Cloud Management Gateway (CMG)  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

Mer information finns i [CMG-portar och data flöde](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow).

### <a name="client----distribution-point-both-standard-and-pull"></a><a name="BKMK_PortsClient-DP"></a> Klient – > distributions plats, både standard och pull  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup> [Anmärkning 2](#bkmk_note2) alternativ port tillgänglig</sup>|  
|HTTPS|--|443 <sup> [Anmärkning 2](#bkmk_note2) alternativ port tillgänglig</sup>|
|Express-uppdateringar|--|8005 <sup> [Anmärkning 2](#bkmk_note2) alternativ port tillgänglig</sup>|<!-- SCCMDocs#2091 -->

> [!NOTE]
> Använd klient inställningar för att konfigurera den alternativa porten för Express uppdateringar. Mer information finns i [port som klienter använder för att ta emot begär Anden om delta innehåll](../../clients/deploy/about-client-settings.md#port-that-clients-use-to-receive-requests-for-delta-content).

### <a name="client----distribution-point-configured-for-multicast-both-standard-and-pull"></a><a name="BKMK_PortsClient-DP2"></a> Klient--> distributions plats som kon figurer ATS för multicast, både standard och pull  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|Multicast-protokoll|63000-64000|--|  

### <a name="client----distribution-point-configured-for-pxe-both-standard-and-pull"></a><a name="BKMK_PortsClient-DP3"></a> Klient--> distributions plats konfigurerad för PXE, både standard och pull  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|DHCP|67 och 68|--|  
|TFTP|69 <sup> [anmärkning 4](#bkmk_note4)</sup> |--|  
|Boot information negotiation layer (BINL)|4011|--|  

> [!Important]  
> Om du aktiverar en värdbaserad brand vägg kontrollerar du att reglerna tillåter att servern skickar och tar emot dem på dessa portar. När du aktiverar en distributions plats för PXE kan Configuration Manager aktivera regler för inkommande (ta emot) i Windows-brandväggen. Den konfigurerar inte utgående regler (skicka).<!--SCCMDocs issue #744-->  

### <a name="client----fallback-status-point"></a><a name="BKMK_PortsClient-FSP"></a> Klient--> återställnings status plats  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup> [Anmärkning 2](#bkmk_note2) alternativ port tillgänglig</sup>|  

### <a name="client----global-catalog-domain-controller"></a><a name="BKMK_PortsClient-GCDC"></a> Klient--> global katalog-domänkontrollant

En Configuration Manager-klient kontaktar inte en global katalog server när den är en arbets grupps dator eller när den har kon figurer ATS för endast Internet-kommunikation.  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|Global katalog LDAP|--|3268|  

### <a name="client----management-point"></a><a name="BKMK_PortsClient-MP"></a> Klient--> hanterings plats  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|Klientmeddelande (standardkommunikation innan HTTP eller HTTPS används som reserv)|--|10123 <sup> [Anmärkning 2](#bkmk_note2) alternativ port tillgänglig</sup>|  
|HTTP|--|80 <sup> [Anmärkning 2](#bkmk_note2) alternativ port tillgänglig</sup>|  
|HTTPS|--|443 <sup> [Anmärkning 2](#bkmk_note2) alternativ port tillgänglig</sup>|  

### <a name="client----software-update-point"></a><a name="BKMK_PortsClient-SUP"></a> Klient--> program uppdaterings plats  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 eller 8530 <sup> [Anmärkning 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 eller 8531 <sup> [Anmärkning 3](#bkmk_note3)</sup>|  

### <a name="client----state-migration-point"></a><a name="BKMK_PortsClient-SMP"></a> Klient--> plats för tillståndsmigrering  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup> [Anmärkning 2](#bkmk_note2) alternativ port tillgänglig</sup>|  
|HTTPS|--|443 <sup> [Anmärkning 2](#bkmk_note2) alternativ port tillgänglig</sup>|  
|Server Message Block (SMB)|--|445|  

### <a name="cmg-connection-point----cmg-cloud-service"></a><a name="bkmk_cmgcp-cmg"></a> CMG-anslutnings punkt – > CMG Cloud service  

Configuration Manager använder dessa anslutningar för att bygga CMG-kanalen. Mer information finns i [CMG-portar och data flöde](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow).

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|TCP-TLS (önskad)|--|10140-10155|  
|HTTPS (fallback med en virtuell dator)|--|443|  
|HTTPS (fallback med två eller flera virtuella datorer)|--|10124-10139|  

### <a name="cmg-connection-point----management-point"></a><a name="bkmk_cmgcp-mp"></a> CMG-anslutnings punkt – > hanterings plats  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|

Mer information finns i [CMG-portar och data flöde](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow).

### <a name="cmg-connection-point----software-update-point"></a><a name="bkmk_cmgcp-sup"></a> CMG-anslutnings punkt--> program uppdaterings plats  

Den aktuella porten är beroende av konfigurationen av program uppdaterings platsen.

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|
|HTTP|--|80|  

Mer information finns i [CMG-portar och data flöde](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow).

### <a name="configuration-manager-console----client"></a><a name="BKMK_PortsConsole-Client"></a> Configuration Manager konsol – > klienten  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|Fjärrstyrning (styrning)|--|2701|  
|Fjärrhjälp (RDP och RTC)|--|3389|  

### <a name="configuration-manager-console----internet"></a><a name="BKMK_PortsConsole-Internet"></a> Configuration Manager-konsol – > Internet  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80|  
|HTTPS|--|443|

Configuration Manager-konsolen använder Internet åtkomst för följande åtgärder:

- Hämta program uppdateringar från Microsoft Update för distributions paket.
- Feedback-objektet i menyfliksområdet.
- Länkar till dokumentationen i-konsolen.
<!--506823-->

### <a name="configuration-manager-console----reporting-services-point"></a><a name="BKMK_PortsConsole-RSP"></a> Configuration Manager-konsol--> repor ting Services-plats  

|Beskrivning|UDP|TCP|
|-----------------|---------|---------|
|HTTP|--|80 <sup> [Anmärkning 2](#bkmk_note2) alternativ port tillgänglig</sup>|  
|HTTPS|--|443 <sup> [Anmärkning 2](#bkmk_note2) alternativ port tillgänglig</sup>|  

### <a name="configuration-manager-console----site-server"></a><a name="BKMK_PortsConsole-Site"></a> Configuration Manager-konsol – > plats Server  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|RPC (ursprunglig anslutning till WMI för att lokalisera ett providersystem)|--|135|  

### <a name="configuration-manager-console----sms-provider"></a><a name="BKMK_PortsConsole-Provider"></a> Configuration Manager-konsol--> SMS-provider  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|RPC-slutpunktsmappare|135|135|  
|RPC|--|DYNAMISK <sup> [anmärkning 6](#bkmk_note6)</sup>|  

### <a name="configuration-manager-network-device-enrollment-service-ndes-policy-module----certificate-registration-point"></a><a name="BKMK_PortsCertificateRegistationPoint_PolicyModule"></a> Princip modul för registrerings tjänsten för nätverks enheter (NDES) – > certifikat registrerings plats Configuration Manager  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443 <sup> [Anmärkning 2](#bkmk_note2) alternativ port tillgänglig</sup>|  

### <a name="data-warehouse-service-point----sql-server"></a><a name="BKMK_PortsDWSPSQL"></a> Informations lager service punkt--> SQL Server  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|SQL över TCP|--|1433 <sup> [Anmärkning 2](#bkmk_note2) alternativ port tillgänglig</sup>|  

### <a name="distribution-point-both-standard-and-pull----management-point"></a><a name="BKMK_PortsDist_MP"></a> Distributions plats, både standard-och pull--> hanterings plats

En distributionsplats kommunicerar med hanteringsplatsen i följande fall:  

- Rapportera status för förinstallerat innehåll  

- För att rapportera användningsöversiktsdata  

- För att rapportera innehållsvalidering  

- Rapportera status för nedladdning av paket (endast mottagar distributions plats)

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup> [Anmärkning 2](#bkmk_note2) alternativ port tillgänglig</sup>|  
|HTTPS|--|443 <sup> [Anmärkning 2](#bkmk_note2) alternativ port tillgänglig</sup>|  

### <a name="endpoint-protection-point----internet"></a><a name="BKMK_PortsEndpointProtection_Internet"></a> Endpoint Protection Point--> Internet  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80|  

### <a name="endpoint-protection-point----sql-server"></a><a name="BKMK_PortsEP-to-SQL"></a> Endpoint Protection Point--> SQL Server  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|SQL över TCP|--|1433 <sup> [Anmärkning 2](#bkmk_note2) alternativ port tillgänglig</sup>|  

### <a name="enrollment-proxy-point----enrollment-point"></a><a name="BKMK_PortsEnrollmentProxyEnrollmentPoint"></a> Proxy för registrerings plats – > registrerings plats  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443 <sup> [Anmärkning 2](#bkmk_note2) alternativ port tillgänglig</sup>|  

### <a name="enrollment-point----sql-server"></a><a name="BKMK_PortsEnrollmentEnrollmentSQL"></a> Registrerings plats – > SQL Server  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|SQL över TCP|--|1433 <sup> [Anmärkning 2](#bkmk_note2) alternativ port tillgänglig</sup>|  

### <a name="exchange-server-connector----exchange-online"></a><a name="BKMK_PortsExchangeConnectorHosted"></a> Exchange Server-koppling – > Exchange Online  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|Windows Remote Management via HTTPS|--|5986|  

### <a name="exchange-server-connector----on-premises-exchange-server"></a><a name="BKMK_PortsExchangeConnectorOnPrem"></a> Exchange Server-koppling – > lokal Exchange Server  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|Windows Remote Management via HTTP|--|5985|  

### <a name="mac-computer----enrollment-proxy-point"></a><a name="BKMK_PortsMacEnrollmentProxyPoint"></a> Mac-dator--> proxy för registrerings plats  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

### <a name="management-point----domain-controller"></a><a name="BKMK_PortsMP-DC"></a> Hanterings plats--> domänkontrollant  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|LDAP (Lightweight Directory Access Protocol)|389|389|  
|Säkert LDAP (LDAPs, för signering och bindning)|636|636|  
|Global katalog LDAP|--|3268|  
|RPC-slutpunktsmappare|--|135|  
|RPC|--|DYNAMISK <sup> [anmärkning 6](#bkmk_note6)</sup>|  

### <a name="management-point-lt---site-server"></a><a name="BKMK_PortsMP-Site"></a> Hanterings plats &lt; – > plats Server

<sup>[Anmärkning 5](#bkmk_note5)</sup>

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|RPC-slutpunktsmappare|--|135|  
|RPC|--|DYNAMISK <sup> [anmärkning 6](#bkmk_note6)</sup>|  
|Server Message Block (SMB)|--|445|  

### <a name="management-point----sql-server"></a><a name="BKMK_PortsMP-SQL"></a> Hanterings plats – > SQL Server  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|SQL över TCP|--|1433 <sup> [Anmärkning 2](#bkmk_note2) alternativ port tillgänglig</sup>|  

### <a name="mobile-device----enrollment-proxy-point"></a><a name="BKMK_PortsMobileDeviceClient-EnrollmentProxyPoint"></a> Mobil enhet--> proxy för registrerings plats  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

###  <a name="reporting-services-point----sql-server"></a><a name="BKMK_PortsRSP-SQL"></a> Repor ting Services-plats – > SQL Server  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|SQL över TCP|--|1433 <sup> [Anmärkning 2](#bkmk_note2) alternativ port tillgänglig</sup>|  

### <a name="service-connection-point----azure-cmg"></a><a name="bkmk_scp-cmg"></a> Tjänst anslutnings punkt--> Azure (CMG)  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS för CMG-tjänst distribution|--|443|

Mer information finns i [CMG-portar och data flöde](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow).

### <a name="site-server-lt---application-catalog-web-service-point"></a><a name="BKMK_PortsAppCatalogWebServicePoint_SiteServer"></a> Plats Server &lt; --> programkatalog webb tjänst punkt  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-slutpunktsmappare|135|135|  
|RPC|--|DYNAMISK <sup> [anmärkning 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---application-catalog-website-point"></a><a name="BKMK_PortsAppCatalogWebSitePoint_SiteServer"></a> Plats Server &lt; --> programkatalog webbplats punkt  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-slutpunktsmappare|135|135|  
|RPC|--|DYNAMISK <sup> [anmärkning 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---asset-intelligence-synchronization-point"></a><a name="BKMK_PortsSite-AISP"></a> Plats Server &lt; --> tillgångsinformation plats för synkronisering  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-slutpunktsmappare|135|135|  
|RPC|--|DYNAMISK <sup> [anmärkning 6](#bkmk_note6)</sup>|  

### <a name="site-server----client"></a><a name="BKMK_PortsSite-Client"></a> Plats Server-->-klient  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|Wake on LAN|9 <sup> [Anmärkning 2](#bkmk_note2) alternativ port tillgänglig</sup>|--|  

### <a name="site-server----cloud-distribution-point"></a><a name="BKMK_PortsSiteServer-CloudDP"></a> Plats Server--> moln distributions plats  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

Mer information finns i [portar och data flöde](use-a-cloud-based-distribution-point.md#bkmk_dataflow).

### <a name="site-server----distribution-point-both-standard-and-pull"></a><a name="BKMK_PortsSite-DP"></a> Plats Server--> distributions plats, både standard och pull

<sup>[Anmärkning 5](#bkmk_note5)</sup>  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-slutpunktsmappare|135|135|  
|RPC|--|DYNAMISK <sup> [anmärkning 6](#bkmk_note6)</sup>|  

### <a name="site-server----domain-controller"></a><a name="BKMK_PortsSite-DC"></a> Plats Server--> domänkontrollant  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|LDAP (Lightweight Directory Access Protocol)|389|389|
|Säkert LDAP (LDAPs, för signering och bindning)|636|636|
|Global katalog LDAP|--|3268|  
|RPC-slutpunktsmappare|--|135|  
|RPC|--|DYNAMISK <sup> [anmärkning 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---certificate-registration-point"></a><a name="BKMK_PortsCertificateRegistrationPoint_SiteServer"></a> Plats Server &lt; --> certifikat registrerings plats  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-slutpunktsmappare|135|135|  
|RPC|--|DYNAMISK <sup> [anmärkning 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---cmg-connection-point"></a><a name="BKMK_CMGCP_SiteServer"></a> Plats Server &lt; --> CMG kopplings punkt

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-slutpunktsmappare|135|135|  
|RPC|--|DYNAMISK <sup> [anmärkning 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---endpoint-protection-point"></a><a name="BKMK_PortsEndpointProtection_SiteServer"></a> Plats Server &lt; --> Endpoint Protection Point  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-slutpunktsmappare|135|135|  
|RPC|--|DYNAMISK <sup> [anmärkning 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---enrollment-point"></a><a name="BKMK_EnrollmentPoint_SiteServer"></a> Plats Server &lt; --> registrerings plats  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-slutpunktsmappare|135|135|  
|RPC|--|DYNAMISK <sup> [anmärkning 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---enrollment-proxy-point"></a><a name="BKMK_EnrollmentProxyPoint_SiteServer"></a> Plats Server &lt; --> proxy för registrerings plats  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-slutpunktsmappare|135|135|  
|RPC|--|DYNAMISK <sup> [anmärkning 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---fallback-status-point"></a><a name="BKMK_PortsSite-FSP"></a> Plats Server &lt; --> återställnings status punkt

<sup>[Anmärkning 5](#bkmk_note5)</sup>  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-slutpunktsmappare|135|135|  
|RPC|--|DYNAMISK <sup> [anmärkning 6](#bkmk_note6)</sup>|  

### <a name="site-server----internet"></a><a name="BKMK_PortSite-Internet"></a> Plats Server--> Internet  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup> [Anmärkning 1](#bkmk_note1)</sup>|  

### <a name="site-server-lt---issuing-certification-authority-ca"></a><a name="BKMK_PortsIssuingCA_SiteServer"></a> Plats Server &lt; --> utfärdande certifikat utfärdare (ca)

Denna kommunikationskanal används när du distribuerar certifikatprofiler genom att använda certifikatregistreringsplatsen. Kommunikationen används inte för varje plats server i hierarkin. I stället används den endast för plats servern längst upp i hierarkin.  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|RPC-slutpunktsmappare|135|135|  
|RPC (DCOM)|--|DYNAMISK <sup> [anmärkning 6](#bkmk_note6)</sup>|  

### <a name="site-server----server-hosting-remote-content-library-share"></a><a name="BKMK_PortsSite-RCL"></a> Plats Server--> server som är värd för fjär innehålls biblioteks resurs

Du kan flytta innehålls biblioteket till en annan lagrings plats för att frigöra hårddisk utrymme på den centrala administrations servern eller den primära plats servern. Mer information finns i [Konfigurera ett fjärrinnehålls bibliotek för plats servern](the-content-library.md#bkmk_remote).

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  

### <a name="site-server-lt---service-connection-point"></a><a name="BKMK_SCP_SiteServer"></a> Plats Server &lt; --> tjänst anslutnings punkt

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-slutpunktsmappare|135|135|  
|RPC|--|DYNAMISK <sup> [anmärkning 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---reporting-services-point"></a><a name="BKMK_PortsSite-RSP"></a> Plats Server &lt; --> repor ting Services-plats

<sup>[Anmärkning 5](#bkmk_note5)</sup>  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-slutpunktsmappare|135|135|  
|RPC|--|DYNAMISK <sup> [anmärkning 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---site-server"></a><a name="BKMK_PortsSite-Site"></a> Plats Server &lt; --> plats Server  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  

### <a name="site-server----sql-server"></a><a name="BKMK_PortsSite-SQL"></a> Plats Server--> SQL Server  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|SQL över TCP|--|1433 <sup> [Anmärkning 2](#bkmk_note2) alternativ port tillgänglig</sup>|  

Under installationen av en plats som använder en fjärran sluten SQL Server för att vara värd för plats databasen öppnar du följande portar mellan plats servern och SQL Server:  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-slutpunktsmappare|135|135|  
|RPC|--|DYNAMISK <sup> [anmärkning 6](#bkmk_note6)</sup>|  

### <a name="site-server----sql-server-for-wsus"></a><a name="BKMK_PortsSite-SQL-WSUS"></a> Plats Server--> SQL Server för WSUS  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|SQL över TCP|--|1433 <sup> [Anmärkning 3](#bkmk_note3) alternativ port tillgänglig</sup>|  

### <a name="site-server----sms-provider"></a><a name="BKMK_PortsSite-Provider"></a> Plats Server--> SMS-provider  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-slutpunktsmappare|135|135|  
|RPC|--|DYNAMISK <sup> [anmärkning 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---software-update-point"></a><a name="BKMK_PortsSite-SUP"></a> Plats Server &lt; --> program uppdaterings plats

<sup>[Anmärkning 5](#bkmk_note5)</sup>  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|HTTP|--|80 eller 8530 <sup> [Anmärkning 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 eller 8531 <sup> [Anmärkning 3](#bkmk_note3)</sup>|  

### <a name="site-server-lt---state-migration-point"></a><a name="BKMK_PortsSite-SMP"></a> Plats Server &lt; --> plats för tillståndsmigrering

<sup>[Anmärkning 5](#bkmk_note5)</sup>  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-slutpunktsmappare|135|135|  

### <a name="sms-provider----sql-server"></a><a name="BKMK_PortsProvider-SQL"></a> SMS-provider – > SQL Server  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|SQL över TCP|--|1433 <sup> [Anmärkning 2](#bkmk_note2) alternativ port tillgänglig</sup>|  

### <a name="software-update-point----internet"></a><a name="BKMK_PortsSUP-Internet"></a> Program uppdaterings plats--> Internet  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup> [Anmärkning 1](#bkmk_note1)</sup>|  

### <a name="software-update-point----upstream-wsus-server"></a><a name="BKMK_PortsSUP-WSUS"></a> Program uppdaterings plats – > Överordnad WSUS-Server  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 eller 8530 <sup> [Anmärkning 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 eller 8531 <sup> [Anmärkning 3](#bkmk_note3)</sup>|  

### <a name="sql-server----sql-server"></a><a name="BKMK_PortsSQL-SQL"></a> SQL Server -- &gt; SQL Server

Databas replikering mellan platser kräver att SQL Server på en plats för att kommunicera direkt med SQL Server på den överordnade eller underordnade platsen.  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|SQL Server tjänst|--|1433 <sup> [Anmärkning 2](#bkmk_note2) alternativ port tillgänglig</sup>|  
|SQL Server Service Broker|--|4022 <sup> [Anmärkning 2](#bkmk_note2) alternativ port tillgänglig</sup>|  

> [!TIP]  
> Configuration Manager kräver inte SQL Server Browser som använder port UDP 1434.  

### <a name="state-migration-point----sql-server"></a><a name="BKMK_PortsStateMigrationPoint-to-SQL"></a> Plats för tillståndsmigrering – > SQL Server  

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|SQL över TCP|--|1433 <sup> [Anmärkning 2](#bkmk_note2) alternativ port tillgänglig</sup>|  

### <a name="notes-for-ports-used-by-configuration-manager-clients-and-site-systems"></a><a name="BKMY_PortNotes"></a> Anmärkningar om portar som används av Configuration Manager-klienter och platssystem  

#### <a name="note-1-proxy-server-port"></a><a name="bkmk_note1"></a> Anmärkning 1: proxyserver-port

Den här porten kan inte konfigureras, men den kan dirigeras via en konfigurerad proxyserver.  

#### <a name="note-2-alternate-port-available"></a><a name="bkmk_note2"></a> Anmärkning 2: alternativ tillgänglig port

Du kan definiera en alternativ port i Configuration Manager för det här värdet. Om du definierar en anpassad port använder du den anpassade porten i IP-filter-informationen för IPsec-principer eller för att konfigurera brand väggar.  

#### <a name="note-3-windows-server-update-services-wsus"></a><a name="bkmk_note3"></a> Anmärkning 3: Windows Server Update Services (WSUS)

WSUS kan installeras för att antingen använda portarna 80/443 eller portarna 8530/8531 för klient kommunikation. När du kör WSUS i Windows Server 2012 eller Windows Server 2016 konfigureras WSUS som standard att använda port 8530 för HTTP och port 8531 för HTTPS.  

Efter installationen kan du byta port. Du behöver inte använda samma port nummer i hela hierarkin.  

- Om HTTP-porten är 80 måste HTTPS-porten vara 443.  

- Om HTTP-porten är något annat måste HTTPS-porten vara 1 eller högre, till exempel 8530 och 8531.

    > [!NOTE]  
    >  När du konfigurerar platsen för programuppdatering som ska använda HTTPS måste HTTP-porten också vara öppen. Okrypterade data, till exempel licensvillkoren för specifika uppdateringar, använder HTTP-porten.

- Plats servern upprättar en anslutning till SQL-servern som är värd för SUSDB när du aktiverar följande alternativ för rensning av WSUS:
  - Lägg till icke-grupperade index i WSUS-databasen för att förbättra prestanda för rensning av WSUS
  - Ta bort föråldrade uppdateringar från WSUS-databasen
  
  Om standard SQL Server porten ändras till en annan port med Konfigurationshanteraren för SQL Server, se till att plats servern kan ansluta med den definierade porten. Configuration Manager stöder inte dynamiska portar. Som standard använder SQL Server namngivna instanser dynamiska portar för anslutningar till databas motorn. När du använder en namngiven instans konfigurerar du den statiska porten manuellt.

#### <a name="note-4-trivial-ftp-tftp-daemon"></a><a name="bkmk_note4"></a> Anmärkning 4: daemon för trivial FTP (TFTP)

Daemon-systemtjänsten för trivial FTP (TFTP) kräver inget användar namn eller lösen ord och är en integrerad del av Windows Deployment Services (WDS). Tjänsten trivial FTP daemon implementerar stöd för TFTP-protokollet som definieras i följande RFC: er:  

- RFC 1350: TFTP  

- RFC 2347: alternativ tillägg  

- RFC 2348: alternativ för block storlek  

- RFC 2349: alternativ för tids gräns och överförings storlek  

TFTP är utformat för att ge stöd för diskbaserade start miljöer. TFTP-demonerna lyssnar på UDP-porten 69 men svarar från en dynamiskt tilldelad högre port. Om du aktiverar den här porten kan TFTP-tjänsten ta emot inkommande TFTP-begäranden, men den valda servern kan inte svara på dessa förfrågningar. Du kan inte aktivera den valda servern för att svara på inkommande TFTP-begäranden om du inte konfigurerar TFTP-servern att svara från Port 69.  

Den PXE-aktiverade distributions platsen och klienten i Windows PE väljer dynamiskt allokerade höga portar för TFTP-överföringar. Dessa portar definieras av Microsoft mellan 49152 och 65535. Mer information finns i [tjänst översikt och krav på nätverks portar för Windows](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows)

Men under den faktiska PXE-starten väljer nätverkskortet på enheten den dynamiskt allokerade hög port som används under TFTP-överföringen. Nätverkskortet på enheten är inte kopplat till de dynamiskt allokerade höga portarna som definierats av Microsoft. Den är bara kopplad till de portar som definieras i RFC 1350. Den här porten kan vara valfri från 0 till 65535. Om du vill ha mer information om vilka dynamiskt allokerade höga portar som nätverkskortet använder kontaktar du enhetens maskin varu tillverkare.

#### <a name="note-5-communication-between-the-site-server-and-site-systems"></a><a name="bkmk_note5"></a> Anmärkning 5: kommunikation mellan plats servern och plats systemen

Kommunikationen mellan plats servern och plats systemen är som standard dubbelriktad. Plats servern startar kommunikationen för att konfigurera plats systemet och sedan ansluter de flesta plats system tillbaka till plats servern för att skicka statusinformation. Repor ting service-platser och distributions platser skickar ingen statusinformation. Om du väljer **kräver att plats servern initierar anslutningar till plats systemet** på plats system egenskaperna efter att plats systemet har installerats, startar inte plats systemet kommunikationen med plats servern. Plats servern startar i stället kommunikationen. Kontot för installation av plats system används för autentisering till plats system servern.  

#### <a name="note-6-dynamic-ports"></a><a name="bkmk_note6"></a> Anmärkning 6: dynamiska portar

Dynamiska portar använder ett intervall med port nummer som definieras av operativ Systems versionen. Dessa portar kallas även tillfälliga portar. Mer information om standardportintervallen finns i [Tjänstöversikt och krav på nätverksportar för Windows Server-systemet](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows).  

## <a name="additional-lists-of-ports"></a><a name="BKMK_AdditionalPorts"></a> Ytterligare port listor  

Följande avsnitt innehåller ytterligare information om portar som Configuration Manager använder.

### <a name="client-to-server-shares"></a><a name="BKMK_ClientShares"></a> Klient till server-resurser

Klienterna använder SMB (Server Message Block) när de ansluter till UNC-resurser. Exempel:

- Manuell klient installation som anger CCMSetup.exe **/Source:** kommando rads egenskap  

- Endpoint Protection klienter som hämtar definitionsfiler från en UNC-sökväg

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  

### <a name="connections-to-microsoft-sql-server"></a><a name="BKMK_SQLPorts"></a> Anslutningar till Microsoft SQL Server

Vid kommunikation med SQL Server-databasmotorn och för replikering mellan platser kan du använda SQL Servers standardport eller ange egna portar:  

- Vid kommunikation mellan platser används:  

  - SQL Server Service Broker med standardporten TCP 4022.  

  - SQL Server tjänst som är som standard port TCP 1433.  

- Kommunikation mellan platser mellan SQL Server databas motor och olika Configuration Manager plats system roller som standard port TCP 1433.  

- Configuration Manager använder samma portar och protokoll för att kommunicera med varje SQL-tillgänglighetsgruppen som är värd för plats databasen som om repliken var en fristående SQL Server instans.

När du använder Azure och plats databasen ligger bakom en intern eller extern belastningsutjämnare konfigurerar du följande komponenter:

- Brand Väggs undantag för varje replik
- Belastnings Utjämnings regler

Konfigurera följande portar:

- SQL över TCP: TCP 1433
- SQL Server Service Broker: TCP 4022
- SMB (Server Message Block): TCP 445
- RPC-slutpunktsmappare: TCP 135

> [!WARNING]  
> Configuration Manager stöder inte dynamiska portar. som standard använder SQL Server namngivna instanser dynamiska portar för anslutningar till databas motorn. När du använder en namngiven instans konfigurerar du den statiska porten för kommunikation mellan platser manuellt.  

Följande platssystemsroller kommunicerar direkt med SQL Server-databasen:  

- Webbservicepunkt för programkatalog  

- Certifikatregistreringsplatsroll  

- Registreringsplatsroll  

- Hanteringsplats  

- Platsserver  

- Rapporteringstjänstpunkt  

- SMS-providern  

- SQL Server--> SQL Server  

När en SQL Server är värd för en databas från mer än en plats måste varje databas använda en separat instans av SQL Server. Konfigurera varje instans med en unik uppsättning portar.  

Om du aktiverar en värdbaserad brand vägg på SQL-servern konfigurerar du den så att den tillåter rätt portar. Konfigurera även nätverks brand väggar på mellan datorer som kommunicerar med SQL Server.  

Ett exempel på hur du konfigurerar SQL Server att använda en speciell port finns i [Konfigurera en server för att lyssna på en angiven TCP-port](/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port).  

### <a name="discovery-and-publishing"></a><a name="bkmk_discovery"> </a> Identifiering och publicering

Configuration Manager använder följande portar för identifiering och publicering av plats information:

- LDAP (Lightweight Directory Access Protocol): 389
- Säkert LDAP (LDAPs, för signering och bindning): 636
- Global katalog LDAP: 3268
- RPC-slutpunktsmappare: 135
- RPC: dynamiskt allokerade hög TCP-portar
- TCP: 1024:5000
- TCP: 49152:65535

### <a name="external-connections-made-by-configuration-manager"></a><a name="BKMK_External"></a> Externa anslutningar som görs av Configuration Manager

Lokala Configuration Manager-klienter eller plats system kan göra följande externa anslutningar:  

- [Tillgångsinformation plats för synkronisering-- &gt; Microsoft](#BKMK_PortsAI)  

- [Endpoint Protection Point-- &gt; Internet](#BKMK_PortsEndpointProtection_Internet)  

- [Klient – domänkontrollant för &gt; Global katalog](#BKMK_PortsClient-GCDC)  

- [Configuration Manager-konsol-- &gt; Internet](#BKMK_PortsConsole-Internet)  

- [Hanterings plats-- &gt; domänkontrollant](#BKMK_PortsMP-DC)  

- [Plats Server &gt; --domänkontrollant](#BKMK_PortsSite-DC)  

- [Plats server som &lt;  -- &gt; utfärdar certifikat utfärdare (ca)](#BKMK_PortsIssuingCA_SiteServer)  

- [Program uppdaterings plats-- &gt; Internet](#BKMK_PortsSUP-Internet)  

- [Program uppdaterings plats – &gt; överordnad WSUS-Server](#BKMK_PortsSUP-WSUS)  

- [Tjänst anslutnings punkt--> Azure](#bkmk_scp-cmg)  

- [CMG-anslutnings punkt – > CMG Cloud service](#bkmk_cmgcp-cmg)  

### <a name="installation-requirements-for-site-systems-that-support-internet-based-clients"></a><a name="BKMK_IBCMports"></a> Installations krav för plats system som stöder Internetbaserade klienter

> [!Note]  
> Det här avsnittet gäller endast för internetbaserad klient hantering (IBCM). Den gäller inte för Cloud Management Gateway. Mer information finns i [Hantera klienter på Internet](../../clients/manage/manage-clients-internet.md).  

Internetbaserade hanterings platser, distributions platser som stöder Internetbaserade klienter, program uppdaterings platsen och återställnings status punkten använder följande portar för installation och reparation:  

- Plats Server--> plats system: RPC-slutpunktsmapparen med UDP och TCP-port 135.  

- Plats Server--> plats system: RPC dynamiska TCP-portar  

- Plats Server &lt; --> plats system: SMB (Server Message Block) med TCP-port 445

Program- och paketinstallationer på distributionsplatser kräver följande RPC-portar:  

- Plats Server--> distributions plats: RPC-slutpunktsmapparen med UDP och TCP-port 135

- Plats Server--> distributions plats: dynamiska RPC-TCP-portar  

Använd IPsec för att säkra trafiken mellan platsservern och platssystemen. Om du måste begränsa de dynamiska portar som används med RPC kan du använda konfigurations verktyget för Microsoft RPC (rpccfg.exe). Använd verktyget för att konfigurera ett begränsat port intervall för de här RPC-paketen. Mer information finns i [så här konfigurerar du RPC så att vissa portar används och hur du skyddar dessa portar med hjälp av IPSec](https://support.microsoft.com/help/908472/how-to-configure-rpc-to-use-certain-ports-and-how-to-help-secure-those).  

> [!IMPORTANT]
> Innan du installerar dessa plats system måste du kontrol lera att Remote Registry-tjänsten körs på plats system servern och att du har angett ett konto för plats system installation om plats systemet finns i en annan Active Directory skog utan en förtroende relation. Fjär register tjänsten används till exempel på servrar som kör plats system som distributions platser (både pull och standard), fjärranslutna SQL-servrar och Programkatalog.

### <a name="ports-used-by-configuration-manager-client-installation"></a><a name="BKMK_PortsClientInstall"></a> Portar som används av Configuration Manager klient installation

De portar som Configuration Manager använder vid klient installation beror på distributions metoden.

- En lista över portar för varje klient distributions metod finns i [portar som används under Configuration Manager klient distribution](../../clients/deploy/windows-firewall-and-port-settings-for-clients.md#ports-used-during-configuration-manager-client-deployment)  

- Mer information om hur du konfigurerar Windows-brandväggen på klienten för klient installation och efter installation av kommunikation finns i [Windows-brandväggen och port inställningar för klienter](../../clients/deploy/windows-firewall-and-port-settings-for-clients.md)  

### <a name="ports-used-by-migration"></a><a name="BKMK_MigrationPorts"></a> Portar som används av migrering

Plats servern som kör migreringen använder flera portar för att ansluta till tillämpliga platser i källhierarkin. Mer information finns i [konfigurationer som krävs för migrering](../../migration/prerequisites-for-migration.md#BKMK_Required_Configurations).  

### <a name="ports-used-by-windows-server"></a><a name="BKMK_ServerPorts"></a> Portar som används av Windows Server

I följande tabell visas några av de viktigaste portarna som används av Windows Server.

|Beskrivning|UDP|TCP|  
|-----------------|---------|---------|  
|DNS|53|53|  
|DHCP|67 och 68|--|  
|NetBIOS-namnmatchning|137|--|  
|NetBIOS-datagramtjänsten|138|--|  
|NetBIOS-sessionstjänsten|--|139|  
|Kerberos-autentisering|--|88|

Mer information finns i följande artiklar:

- [Tjänst översikt och krav på nätverks portar för Windows Server-systemet](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows)

- [Så här konfigurerar du en brand vägg för domäner och förtroenden](https://support.microsoft.com/help/179442/how-to-configure-a-firewall-for-domains-and-trusts)