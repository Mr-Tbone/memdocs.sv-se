---
title: Configuration Manager-verktyg
titleSuffix: Configuration Manager
description: Lär dig mer om de verktyg som hjälper dig att hantera och felsöka Configuration Manager-infrastrukturen.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 395403dc-6997-4415-93fd-6b1eeb6ba31a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: cb2529dbbe923a5035f0b7586dab696cd6fc917e
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699423"
---
# <a name="configuration-manager-tools"></a>Configuration Manager-verktyg

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Managers verktygen omfattar [klientbaserade](#client-tools) och [serverbaserade verktyg](#server-tools). Använd dessa verktyg för att hjälpa till med att stödja och felsöka Configuration Manager-infrastrukturen.

Från och med Configuration Manager version 1806 ingår dessa verktyg i `CD.Latest\SMSSETUP\Tools` mappen på plats servern. Ingen ytterligare installation krävs.<!--1357145--> Använd de här versionerna av verktygen med Configuration Manager version 1806 och senare.

Alla Windows-operativsystem som har stöd för klienter i [operativ system som stöds för klienter och enheter](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices) stöds för användning med dessa verktyg.

> [!Note]  
> [System Center 2012 R2 Configuration Manager Toolkit](https://www.microsoft.com/download/details.aspx?id=50012) är fortfarande tillgängligt från Microsoft Download Center. För Configuration Manager version 1806 och senare använder du versionerna av verktygen på CD: n. Den senaste mappen på plats servern. Vissa verktyg fanns tidigare i Toolkit men ingår inte i version 1806. Dessa äldre verktyg stöds inte längre.


## <a name="client-tools"></a>Klient verktyg

Dessa verktyg finns i `ClientTools` undermappen:

- [CMTrace](cmtrace.md): Visa, övervaka och analysera Configuration Manager loggfiler  

- [Klient-spion](clispy.md): Felsök problem som rör program varu distribution, inventering och mätning

- [Verktyg för distributions övervakning](deployment-monitoring-tool.md): felsöka program, uppdateringar och bas linje distributioner  

- [Princip spion](policy-spy.md): Visa princip tilldelningar  

- [Power Viewer-verktyg](power-viewer-tool.md): Visa status för energispar funktioner  

- [Verktyget Skicka schema](send-schedule-tool.md): utlöser scheman och utvärderingar av konfigurations bas linjer  

> [!Note]  
> `ClientTools`Mappen innehåller också filen Microsoft.Diagnostics.Tracing.EventSource.dll. Flera klient verktyg kräver det här biblioteket. Du kan inte använda den direkt.  


## <a name="server-tools"></a>Server verktyg

Dessa verktyg finns i `ServerTools` undermappen:

- [DP job queue Manager](dp-job-manager.md): fel sökning av innehålls distributions jobb till distributions platser  

- [Visnings program för samlings utvärdering](ceviewer.md): Visa utvärderings information för samlingen  

- [Innehålls biblioteks Utforskaren](content-library-explorer.md): Visa innehåll i det enskilda instans arkivet för innehålls bibliotek  

- [Innehålls biblioteks överföring](content-library-transfer.md): överför innehålls bibliotek mellan enheter  

- [Verktyget för innehålls ägarskap](content-ownership-tool.md): ändrar ägarskap för överblivna paket. Dessa paket finns på platsen utan en ägande plats Server.

- [Rollbaserad administration och gransknings verktyg](rbaviewer.md): hjälper administratörer att granska konfigurationen av roller  

- [Kör](run-meter-summ.md)sammanfattnings verktyget för mätare: kör sammanfattnings aktiviteten för avläsning och analysera avläsnings data

> [!Note]  
> Mappen ServerTools innehåller också följande filer:
>
> - AdminUI.WqlQueryEngine.dll
> - Microsoft.ConfigurationManagement.ManagementProvider.dll
> - Microsoft.Diagnostics.Tracing.EventSource.dll
>
> Flera Server verktyg kräver dessa bibliotek. Du kan inte använda dem direkt.  

## <a name="other-tools-and-toolkits"></a>Andra verktyg och verktygs verktyg

- [Support Center](support-center.md): samla in information från klienter för enklare analys vid fel sökning.

    Från och med version 1906 är **OneTrace** ett nytt logg visnings program med Support Center. Det fungerar ungefär som CMTrace, med förbättringar. Mer information finns i [Support Center OneTrace](support-center-onetrace.md).

- [Utöka och migrera lokala platser till Microsoft Azure](azure-migration-tool.md): hjälper dig att program mässigt skapa virtuella Azure-datorer (VM) för Configuration Manager. <!--3556022--> 

- [Rensnings verktyg för innehålls bibliotek](../plan-design/hierarchy/content-library-cleanup-tool.md): Använd **ContentLibraryCleanup.exe** i `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` om du vill ta bort överblivna innehåll från en distributions plats.  

- [Verktyget underhåll av hierarki](../servers/manage/hierarchy-maintenance-tool-preinst.exe.md): Använd **Preinst.exe** i den `\<SiteServerName>\SMS_<SiteCode>\bin\X64\00000409` delade mappen på plats servern för att skicka kommandon till hierarki Manager-komponenten.  

- [Uppdatera återställnings verktyget](../servers/manage/update-reset-tool.md): Använd **CMUpdateReset.exe** i `CD.Latest\SMSSETUP\TOOLS\CMUpdateReset` för att åtgärda problem när uppdateringar i konsolen har problem med att hämta eller replikera.  

- [Tjänst anslutnings verktyg](../servers/manage/hierarchy-maintenance-tool-preinst.exe.md): Använd **ServiceConnectionTool.exe** i `CD.Latest\SMSSETUP\TOOLS\ServiceConnectionTool` för att hålla platsen uppdaterad när tjänst anslutnings punkten är offline.   

- [Microsoft Deployment Toolkit (MDT)](../../mdt/use-the-mdt.md): en samling verktyg, processer och vägledning för automatisering av distributioner av Desktop-och Server-operativsystem.

- [System Center Updates Publisher (SCUP)](../../sum/tools/updates-publisher.md): ett fristående verktyg för att hantera och importera anpassade program uppdateringar.

- [Package Conversion Manager](../../apps/pcm/package-conversion-manager.md): konvertera äldre paket till program.