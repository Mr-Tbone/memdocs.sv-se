---
title: Support Center
titleSuffix: Configuration Manager
description: Felsök Configuration Manager-klienter med Support Center.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c631197d-7daa-4faa-9e22-980cd6d604c2
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: da2fe2ad66617ffb5ad3058011f111b0aaf9e9ae
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82903916"
---
# <a name="support-center-for-configuration-manager"></a>Support Center för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

<!--1357489-->
Från och med version 1810 använder du Support Center för klient fel sökning, real tids logg visning eller fångar status för en Configuration Manager klient dator för senare analys. Support Center är ett enda verktyg för att konsolidera många administratörs fel söknings verktyg.


## <a name="about"></a>Om

Support Center syftar till att minska utmaningarna och när du felsöker Configuration Manager klient datorer. När du arbetar med support för att lösa ett problem med Configuration Manager-klienter skulle du tidigare behöva samla in loggfiler och annan information manuellt för att felsöka problemet. Det var lätt att glömma en viktig loggfil, vilket leder till ytterligare problem för dig och den support personal som du arbetar med.

Använd Support Center för att effektivisera support upplevelsen. Det gör att du kan:

- Skapa ett fel söknings paket (zip-fil) som innehåller Configuration Manager-klientens loggfiler. Sedan har du en enda fil som du kan skicka till support personal.  

- Visa Configuration Manager klientens loggfiler, certifikat, register inställningar, fel söknings dum par, klient principer.  

- Real tids diagnostik av inventering (ersätter ContentSpy), princip (ersätter PolicySpy) och klientcachen.  

### <a name="support-center-viewer"></a>Support Center Viewer

Support Center innehåller Support Center Viewer, ett verktyg som stöder personal användning för att öppna paketet med filer som du skapar med Support Center. Data insamlaren för Support Center samlar in och paketerar diagnostikloggar från en lokal eller fjärran sluten Configuration Manager klient. Om du vill visa data insamlings paket använder du visnings programmet.

### <a name="support-center-log-file-viewer"></a>Logg fils visnings program för Support Center

Support Center innehåller ett modernt logg visnings program. Det här verktyget ersätter CMTrace och ger ett anpassningsbart gränssnitt med stöd för flikar och docknings bara fönster. Det har ett snabb presentations lager och kan läsa in stora loggfiler på några sekunder.

### <a name="support-center-onetrace-preview"></a>Support Center OneTrace (förhandsversion)

<!--3555962-->
Från och med version 1906 är **OneTrace** ett nytt logg visnings program med Support Center. Det fungerar ungefär som CMTrace, med förbättringar. Mer information finns i [Support Center OneTrace](support-center-onetrace.md).

### <a name="powershell-cmdlets"></a>PowerShell-cmdletar

Support Center innehåller också [PowerShell-cmdletar](https://docs.microsoft.com/powershell/sccm/overview?view=sccm-ps). Använd dessa cmdletar för att skapa en fjärr anslutning till en annan Configuration Manager-klient, för att konfigurera data insamlings alternativ och för att starta data insamling.


## <a name="prerequisites"></a>Förutsättningar

Installera följande komponenter på den server eller klient dator där du installerar Support Center:

- En OS-version som stöds av Configuration Manager. Mer information finns i [OS-versioner som stöds för-klienter](../plan-design/configs/supported-operating-systems-for-clients-and-devices.md). Support Center stöder inte mobila enheter.  

- .NET Framework 4.5.2 krävs på den dator där du kör Support Center och dess komponenter.  


## <a name="install"></a>Installera

Hitta installations programmet för Support Center på plats servern på följande sökväg: `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi` .

När du har installerat den hittar du följande objekt på Start-menyn i **Microsoft System Center** -gruppen:  

- Support Center (ConfigMgrSupportCenter. exe)  
- Logg fils visaren för Support Center (CMLogViewer. exe)  
- Support Center Viewer (ConfigMgrSupportCenterViewer. exe)  


## <a name="known-issues"></a>Kända problem

### <a name="you-cant-install-the-latest-version-if-an-older-version-is-already-installed"></a>Du kan inte installera den senaste versionen om en äldre version redan är installerad

<!--SCCMDocs-pr issue #3090-->
*Gäller för version 1810 och 1902*

Om du redan har installerat en äldre version av Support Center Miss lyckas det nya installations programmet. Det här problemet beror på hur filerna är versioner av den ursprungliga versionen och den senaste versionen. Undvik det här problemet genom att avinstallera den äldre versionen av Support Center först. Installera sedan den senaste versionen.

### <a name="remote-connections-must-include-computer-name-or-domain-as-part-of-the-user-name"></a>Fjärr anslutningar måste innehålla dator namn eller domän som en del av användar namnet

Om du ansluter till en fjärran sluten klient från Support Center måste du ange dator namn eller domän namn för användar kontot när anslutningen upprättas. Om du använder ett kort dator namn eller domän namn (till exempel `.\administrator` ), lyckas anslutningen, men Support Center samlar inte in data från klienten.

Undvik det här problemet genom att använda följande format för användar namn för att ansluta till en fjärran sluten klient:

- `ComputerName\UserName`  
- `DomainName\UserName`  

### <a name="scripted-server-message-block-connections-to-remote-clients-might-require-removal"></a>Skriptbaserade Server Message Block-anslutningar till fjärrklienter kan kräva borttagning

När du ansluter till fjärrklienter med hjälp av PowerShell-cmdleten [New-CMMachineConnection](https://go.microsoft.com/fwlink/p/?linkid=390542) skapar Support Center en SMB-anslutning (Server Message Block) till varje fjärran sluten klient. Dessa anslutningar behålls när du har slutfört data insamlingen. För att undvika att överskrida det maximala antalet fjärr anslutningar för Windows kan du använda `net use` kommandot för att se den aktiva uppsättningen fjärr anslutningar. Inaktivera sedan alla onödiga anslutningar med hjälp av följande kommando:`net use <connection_name> /d`
där `<connection_name>` är namnet på fjärr anslutningen.

### <a name="application-deployment-evaluation-cycle-request-isnt-sent-correctly-to-remote-machines"></a>Begäran om utvärderings cykel för program distribution skickas inte korrekt till fjärrdatorer

<!--2849356-->
*Gäller för version 1810*

Om du i Support Center väljer **utvärdering av program distribution** från åtgärden **anropa utlösare** på fliken **innehåll** startar den här åtgärden en aktivitet som utvärderar distribuerade program. Om du är ansluten till en lokal klient utvärderar den både dator-och användar program distributioner. Om du är ansluten till en fjärran sluten klient utvärderar den dock bara dator programmets distributioner.


## <a name="next-steps"></a>Nästa steg

[Snabb start för Support Center](support-center-quickstart.md)
