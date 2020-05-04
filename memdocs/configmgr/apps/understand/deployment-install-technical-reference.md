---
title: Teknisk referens för program installation
titleSuffix: Configuration Manager
description: Felsöka teknisk referens för programinstallationer för Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 2af4f9c3-16b8-4691-a59d-aea6241d288e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 13c96e9ad4f0608084d87bed3973221730cb2d5f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709784"
---
# <a name="application-installation"></a>Programinstallation

*Gäller för: Configuration Manager (aktuell gren)*

Innan du fortsätter kan du granska [program distributionens klient komponenter](client-components-technical-reference.md) för att förstå jobb bearbetning av DCM-och CI-agenten.

Programinstallationen utförs av DCM agent-och CI agent-komponenter när distributionen tillämpas. Tillämpnings tiden skiljer sig åt för tillgängliga och nödvändiga distributioner. Information om när tilldelningen tillämpas finns i artikeln [program distribution till enhets samlingar](device-deployment-technical-reference.md) eller [program distribution till användar samlingar](user-deployment-technical-reference.md) .

## <a name="enforcement-initiation"></a>Tvångs initiering

Programinstallationen initieras av CI Agent-komponenten på klienten under **StateEnforcingCIs** -fasen. Den här processen är densamma oavsett om programmet distribueras till en enhets samling eller en användar samling.

- För **tillgängliga** distributioner installeras programmet när användaren initierar programinstallationen från Software Center.
- För **nödvändiga** distributioner installeras programmet vid distributionens tids gräns. Användaren kan dock starta installationen från Software Center före tids gränsen.

När CI-agenten startar programinstallationen skapas en aktivitet som hanteras av komponenten CI Task Manager. CI Task Manager initierar sedan installationen. Den här aktiviteten kan spåras i **CITaskMgr. log** med hjälp av ett unikt ID för distributions typen.

<pre><code class="lang-text"><b>Initiating task Enforce</b> for CI ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2 (ConfigMgr Toolkit - Windows Installer (*.msi file)) for target: , consumer: {9BC3154A-98F1-4595-A967-173D536A3F94}
Initiated application enforcement. : CITask(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2..Install.Enforce)
</code></pre>

## <a name="application-enforcement"></a>Program tillämpning

När tillämpnings programmet har startats utför klienten program identifieringen igen för att se till att programmet inte redan är installerat. När programmet har bestämt att programmet inte är installerat, initieras programinstallationen. Den här aktiviteten kan spåras i **AppEnforce. log** på klienten med hjälp av det unika ID: t för distributions typen.

```text
+++ Starting Install enforcement for App DT "ConfigMgr Toolkit - Windows Installer (*.msi file)" ApplicationDeliveryType - ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, Revision - 2, ContentPath - C:\WINDOWS\ccmcache\2, Execution Context - System
    Executing Command line: "C:\WINDOWS\system32\msiexec.exe" /i "ConfigMgrTools.msi" /q /qn with user context
    Process 7292 terminated with exitcode: 0
Status is switching to Success
```

## <a name="installation-verification"></a>Installations verifiering

När programmet har installerats används program identifierings metoden igen för att säkerställa att programmet har identifierats som installerat.

<pre><code class="lang-text">Performing detection of app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
+++ <b>Discovered MSI application</b> [AppDT Id: ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, Revision: 2, MSI Product code: {4FFF7ECC-CCF7-4530-B938-E7812BB91186}, MSI Product version: ]
++++++ <b>App enforcement completed</b> (3 seconds) for App DT "ConfigMgr Toolkit - Windows Installer (*.msi file)" [ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44], Revision: 2, User SID: ] ++++++
</code></pre>

Slutligen, efter att verkställigheten har slutförts, tar CI-agenten emot meddelandet om slutförd uppgift och CI Agent-jobbet flyttas till nästa fas.

<pre><code class="lang-text">CIAgentJob({2BF84225-C9E8-49A6-A308-A160C4B799D3}): CAgentJob::HandleEvent(<b>Event=CITaskComplete, CurrentState=StateEnforcingCIs</b>)
</code></pre>

## <a name="next-steps"></a>Nästa steg

[Felsöka program distributioner](../deploy-use/troubleshoot-application-deployment.md)
