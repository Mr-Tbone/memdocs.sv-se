---
title: Aktivera Transport Layer Security (TLS) 1,2 på plats servrarna och fjärrplatsens system
titleSuffix: Configuration Manager
description: Information om hur du aktiverar TLS 1,2 för Configuration Manager plats servrar.
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0ce9b428-cb0f-46f3-bf69-c465e6623d6f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 15377520b76b9b3a3813e6ad4253548f29e011db
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720550"
---
# <a name="how-to-enable-tls-12-on-the-site-servers-and-remote-site-systems"></a>Så här aktiverar du TLS 1,2 på plats servrar och fjärranslutna plats system

*Gäller för: Configuration Manager (Current Branch)*

När du aktiverar TLS 1,2 för Configuration Managers miljön börjar du med att [Aktivera tls 1,2 för klienterna](enable-tls-1-2-client.md) först. Sedan aktiverar du TLS 1,2 på plats servrarna och fjärrplatssystemet. Testa till sist klient till plats system kommunikation innan du kan inaktivera de äldre protokollen på Server sidan. Följande uppgifter krävs för att aktivera TLS 1,2 på plats servrarna och fjärrplatssystem:

- Se till att TLS 1,2 är aktiverat som ett protokoll för SChannel på operativ system nivå
- Uppdatera och konfigurera .NET Framework för att stödja TLS 1,2
- Uppdatera SQL Server-och klient komponenter
- Uppdaterings Windows Server Update Services (WSUS)

Mer information om beroenden för vissa Configuration Manager funktioner och scenarier finns i [Aktivera TLS 1,2](enable-tls-1-2.md). 

## <a name="ensure-that-tls-12-is-enabled-as-a-protocol-for-schannel-at-the-operating-system-level"></a><a name="bkmk_protocol"></a>Se till att TLS 1,2 är aktiverat som ett protokoll för SChannel på operativ system nivå

[!INCLUDE [Enable TLS 1.2 protocol as a security provider](includes/enable-tls-1-2-protocol-security-provider.md)]

## <a name="update-and-configure-the-net-framework-to-support-tls-12"></a><a name="bkmk_net"></a>Uppdatera och konfigurera .NET Framework för att stödja TLS 1,2

[!INCLUDE [Update and configure the .NET framework to support TLS 1.2](includes/update-net-framework-to-support-tls-1-2.md)]


## <a name="update-sql-server-and-client-components"></a><a name="bkmk_sql"></a>Uppdatera SQL Server-och klient komponenter

Microsoft SQL Server 2016 och senare har stöd för TLS 1,1 och TLS 1,2. Tidigare versioner och beroende bibliotek kan kräva uppdateringar. Mer information finns i [KB 3135244: TLS 1,2-stöd för Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server).

Sekundära plats servrar måste använda minst SQL Server 2016 Express med Service Pack 2 (13.2.50.26) eller senare.

### <a name="sql-server-native-client"></a><a name="bkmk_sql-client"></a>SQL Server Native Client

> [!NOTE]
> [KB 3135244](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server) beskriver också kraven för SQL Server klient komponenter.

Se till att även uppdatera SQL Server Native Client till minst version SQL 2012 SP4 (11. *. 7001.0). Från och med version 1810 är det här kravet en [krav kontroll (varning)](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

Configuration Manager använder SQL Server Native Client på följande plats system roller:

- Platsdatabasserver
- Plats Server: Central administrations webbplats, primär plats eller sekundär plats
- Hanteringsplats
- Enhets hanterings plats
- Plats för tillståndsmigrering
- SMS-provider
- Programuppdateringsplats
- Multicast-aktiverad distributionsplats
- Tillgångsinformation uppdaterings tjänst punkt
- Rapporteringstjänstpunkt
- Webb tjänst för program katalog
- Registreringsplats
- Plats för slutpunktsskydd
- Tjänstanslutningspunkt
- Certifikatregistreringsplats
- Informations lager service punkt


## <a name="update-windows-server-update-services-wsus"></a><a name="bkmk_wsus"></a>Uppdaterings Windows Server Update Services (WSUS)

Om du vill ha stöd för TLS 1,2 i tidigare versioner av WSUS installerar du följande uppdatering på WSUS-servern:

- För WSUS-server som kör Windows Server 2012 installerar du [uppdatering 4022721](https://support.microsoft.com/help/4022721) eller en senare Samlad uppdatering.
- För WSUS-server som kör Windows Server 2012 R2 installerar du [uppdatering 4022720](https://support.microsoft.com/help/4022720) eller en senare Samlad uppdatering.

Från och med Windows Server 2016 stöds TLS 1,2 som standard för WSUS.  TLS 1,2-uppdateringar behövs bara på WSUS-servrar med Windows Server 2012 och Windows Server 2012 R2.

## <a name="next-steps"></a>Nästa steg

- [Vanliga problem vid aktivering av TLS 1.2](enable-tls-1-2-troubleshoot.md)
