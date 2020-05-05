---
title: Aktivera Transport Layer Security (TLS) 1,2 – Översikt
titleSuffix: Configuration Manager
description: Översikt över hur du aktiverar TLS 1,2 för Configuration Manager.
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 31de47c9-891b-4de7-8d5e-fbbc1bff7c60
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5d9d7cea7e5653b338a3eb4adb01d9fded99035e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720522"
---
# <a name="how-to-enable-tls-12"></a>Så här aktiverar du TLS 1,2

*Gäller för: Configuration Manager (Current Branch)*

Transport Layer Security (TLS), som Secure Sockets Layer (SSL), är ett krypterings protokoll som är avsett att skydda data vid överföring över ett nätverk. De här artiklarna beskriver de steg som krävs för att säkerställa att Configuration Manager säker kommunikation använder TLS 1,2-protokollet. De här artiklarna beskriver också uppdaterings krav för vanliga komponenter och fel sökning av vanliga problem.

## <a name="enabling-tls-12"></a>Aktiverar TLS 1,2

Configuration Manager förlitar sig på ett antal olika komponenter för säker kommunikation. Det protokoll som används för en specifik anslutning beror på funktionerna i de relevanta komponenterna på både klienten och Server sidan. Om någon komponent är inaktuell eller inte korrekt konfigurerad, kan kommunikationen använda ett äldre, mindre säkert protokoll. För att korrekt aktivera Configuration Manager att stödja TLS 1,2 för all säker kommunikation måste du Aktivera TLS 1,2 för alla nödvändiga komponenter. De komponenter som krävs beror på din miljö och de Configuration Manager funktioner som du använder.

> [!IMPORTANT]
> Starta den här processen med-klienter, särskilt tidigare versioner av Windows. Innan du aktiverar TLS 1,2 och inaktiverar de äldre protokollen på Configuration Manager servrar, se till att alla klienter stöder TLS 1,2. Annars kan klienterna inte kommunicera med servrarna och de kan vara överblivna.


## <a name="tasks-for-configuration-manager-clients-site-servers-and-remote-site-systems"></a>Aktiviteter för Configuration Manager-klienter, plats servrar och fjärrplatssystem

Om du vill aktivera TLS 1,2 för komponenter som Configuration Manager är beroende av för säker kommunikation måste du utföra flera aktiviteter både på klienterna och på plats servrarna.

### <a name="enable-tls-12-for-configuration-manager-clients"></a>Aktivera TLS 1,2 för Configuration Manager klienter

- [Uppdatera Windows och WinHTTP på Windows 8,0, Windows Server 2012 (ej R2) och tidigare](enable-tls-1-2-client.md#bkmk_winhttp)
- [Se till att TLS 1,2 är aktiverat som ett protokoll för SChannel på operativ system nivå](enable-tls-1-2-client.md#bkmk_protocol)
- [Uppdatera och konfigurera .NET Framework för att stödja TLS 1,2](enable-tls-1-2-client.md#bkmk_net)


### <a name="enable-tls-12-for-configuration-manager-site-servers-and-remote-site-systems"></a>Aktivera TLS 1,2 för Configuration Manager plats servrar och fjärrplatssystem

- [Se till att TLS 1,2 är aktiverat som ett protokoll för SChannel på operativ system nivå](enable-tls-1-2-server.md#bkmk_protocol)
- [Uppdatera och konfigurera .NET Framework för att stödja TLS 1,2](enable-tls-1-2-server.md#bkmk_net)
- [Uppdatera SQL Server och SQL Native Client](enable-tls-1-2-server.md#bkmk_sql)
- [Uppdaterings Windows Server Update Services (WSUS)](enable-tls-1-2-server.md#bkmk_wsus)


## <a name="features-and-scenario-dependencies"></a>Funktioner och scenario beroenden

I det här avsnittet beskrivs beroenden för vissa Configuration Manager funktioner och scenarier. För att fastställa nästa steg, letar du upp de objekt som gäller för din miljö.

|Funktion eller scenario|Uppdatera aktiviteter|
|--- |--- |
|Plats servrar (Central, primär eller sekundär)| - [Uppdatera .NET Framework](enable-tls-1-2-server.md#bkmk_net)<br/> – Kontrol lera starka kryptografi inställningar|
|Platsdatabasserver|[Uppdatera SQL Server och dess klient komponenter](enable-tls-1-2-server.md#bkmk_sql)|
|Sekundära plats servrar|[Uppdatera SQL Server och dess klient komponenter](enable-tls-1-2-server.md#bkmk_sql) till en kompatibel version av SQL Express|
|Platssystemroller| - [Uppdatera .NET Framework](enable-tls-1-2-server.md#bkmk_net) och verifiera starka kryptografi inställningar <br/> - [Uppdatera SQL Server och dess klient komponenter](enable-tls-1-2-server.md#bkmk_sql) på roller som kräver det, inklusive [SQL Server Native Client](enable-tls-1-2-server.md#bkmk_sql-client)|
|Rapporteringstjänstpunkt|- [Uppdatera .NET Framework](enable-tls-1-2-server.md#bkmk_net) på plats servern, SQL Reporting Services-servrar och alla datorer med konsolen<br/> – Starta om tjänsten SMS_Executive om det behövs|
|Programuppdateringsplats|[Uppdatera WSUS](enable-tls-1-2-server.md#bkmk_wsus)|
|Gateway för molnhantering|[Framtvinga TLS 1,2](../../clients/manage/cmg/security-and-privacy-for-cloud-management-gateway.md#bkmk_tls)|
|Configuration Manager-konsolen| - [Uppdatera .NET Framework](enable-tls-1-2-client.md#bkmk_net)<br/> – Kontrol lera starka kryptografi inställningar|
|Configuration Manager-klient med HTTPS-plats system roller|[Uppdatera Windows så att det stöder TLS 1,2 för klient-server-kommunikation med hjälp av WinHTTP](enable-tls-1-2-client.md#bkmk_winhttp)|
|Software Center| - [Uppdatera .NET Framework](enable-tls-1-2-client.md#bkmk_net)<br/> – Kontrol lera starka kryptografi inställningar|
|Windows 7-klienter| *Innan* du aktiverar TLS 1,2 på alla Server komponenter [uppdaterar du Windows så att det stöder TLS 1,2 för klient-server-kommunikation med hjälp av WinHTTP](enable-tls-1-2-client.md#bkmk_winhttp). Om du aktiverar TLS 1,2 på Server komponenter först kan du överblivna tidigare versioner av klienter.|

## <a name="frequently-asked-questions"></a>Vanliga frågor och svar

### <a name="why-use-tls-12-with-configuration-manager"></a>Varför ska jag använda TLS 1,2 med Configuration Manager?

TLS 1,2 är säkrare än tidigare kryptografiska protokoll som SSL 2,0, SSL 3,0, TLS 1,0 och TLS 1,1. TLS 1,2 skyddar i själva verket data som överförs över nätverket.

### <a name="where-does-configuration-manager-use-encryption-protocols-like-tls-12"></a>Var Configuration Manager använda krypterings protokoll som TLS 1,2?

Det finns i princip fem områden som Configuration Manager använder krypterings protokoll som TLS 1,2:

- Klient kommunikation till IIS-baserade plats Server roller när rollen har kon figurer ATS för att använda HTTPS. Exempel på dessa roller är distributions platser, program uppdaterings platser och hanterings platser.
- Hanterings plats, SMS Executive och SMS-provider kommunikation med SQL. Configuration Manager krypterar alltid SQL-kommunikation.
- Plats Server till WSUS-kommunikation om WSUS har kon figurer ATS för att använda HTTPS.
- Configuration Manager-konsolen till SQL Reporting Services (SSRS) om SSRS har kon figurer ATS för att använda HTTPS.
- Alla anslutningar till Internetbaserade tjänster. Exempel på detta är CMG (Cloud Management Gateway), synkronisering av tjänst anslutnings punkt och synkronisering av metadata för uppdatering från Microsoft Update.

### <a name="what-determines-which-encryption-protocol-is-used"></a>Vad avgör vilket krypterings protokoll som används?

HTTPS kommer alltid att förhandla om den högsta protokoll versionen som stöds av både klienten och servern i en krypterad konversation. När en anslutning upprättas skickar klienten ett meddelande till servern med det högsta tillgängliga protokollet. Om servern har stöd för samma version, skickar den ett meddelande med den versionen. Den här förhandlade versionen är den som används för anslutningen. Om servern inte stöder den version som presenteras av klienten, anger Server meddelandet den högsta version som den kan använda. Mer information om TLS Handshake-protokollet finns i [upprätta en säker session med hjälp av TLS](https://docs.microsoft.com/windows/win32/secauthn/tls-handshake-protocol#establishing-a-secure-session-by-using-tls).

### <a name="what-determines-which-protocol-version-the-client-and-server-can-use"></a>Vad avgör vilken protokoll version som klienten och servern kan använda?

I allmänhet kan följande objekt avgöra vilken protokoll version som används:

- Programmet kan diktera vilka specifika protokoll versioner som ska förhandlas.
  - Bästa praxis är att undvika hårda protokoll versioner på program nivå och att följa den konfiguration som definierats på protokoll nivå för komponenter och operativ system.
  - Configuration Manager följer den här rekommenderade metoden.
- För program som skrivs med .NET Framework är standard protokoll versionerna beroende av vilken version av ramverket de kompilerades på.  
  - .NET-versioner före 4.6.3 inkluderar inte TLS 1,1 och 1,2 i listan över protokoll för förhandling, som standard.
- Program som använder WinHTTP för HTTPS-kommunikation, t. ex. Configuration Manager-klienten, är beroende av operativ systemets version, korrigerings nivå och konfiguration för protokoll versions stöd.


## <a name="additional-resources"></a>Ytterligare resurser

- [Teknisk referens för kryptografiska kontroller](cryptographic-controls-technical-reference.md)
- [Metod tips för TLS (Transport Layer Security) med .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry)
- [KB 3135244: TLS 1,2 stöd för Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)

## <a name="next-steps"></a>Nästa steg

- [Aktivera TLS 1.2 på klienter](enable-tls-1-2-client.md)
- [Aktivera TLS 1,2 på plats servrarna](enable-tls-1-2-server.md)
