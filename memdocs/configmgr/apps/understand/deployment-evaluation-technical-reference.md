---
title: Teknisk referens för program utvärdering
titleSuffix: Configuration Manager
description: Felsöka teknisk referens för program utvärdering för Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: a7035223-d7bd-47b4-896f-08de3416a4eb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fdeec54489adfc0d2a5cceb99c7e7587ce1a41ab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709798"
---
# <a name="application-deployment-evaluation"></a>Utvärdering av program distribution

*Gäller för: Configuration Manager (aktuell gren)*

Innan du fortsätter kan du granska [program distributionens klient komponenter](client-components-technical-reference.md) för att förstå jobb bearbetning av DCM-och CI-agenten.

Program utvärdering utförs av DCM-agenten och CI agent-komponenterna när distributionen aktive ras. Information om hur du aktiverar tilldelningen finns i artikeln [program distribution till enhets samlingar](device-deployment-technical-reference.md) eller [program distribution till användar samlingar](user-deployment-technical-reference.md) .

## <a name="application-detection-and-evaluation"></a>Program identifiering och utvärdering

Program utvärdering utförs under **InvokingSdmMethod** -fasen i ett CI Agent-jobb. Den här fasen är den plats där klienten utvärderar den identifierings metod som definierats för programmet för att avgöra om programmet är installerat på enheten. Den här aktiviteten kan spåras i **AppDiscovery. log** med hjälp av distributions typens unika ID eller distributions typens namn.

```text
Performing detection of app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
+++ Did not detect app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
```

> [!NOTE]
> Exemplet ovan visar identifiering för ett MSI-program där identifieringen görs genom att kontrol lera om MSI-produktnyckeln är installerad på enheten. För program som använder alternativa identifierings metoder används lämplig identifierings metod för att kontrol lera om programmet är installerat.

Sedan utvärderar klienten det önskade läget för programmet baserat på distributions syftet. Det här steget innebär också att upptäcka om programmet har några beroenden eller ersättnings regler som ska användas för programmet. Den här aktiviteten kan spåras i **AppIntentEval. log** med hjälp av ett unikt ID för program-och distributions typen.

<pre><code class="lang-text"># Available Application Deployment

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = Applicable, ResolvedState = Available</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]

# Required Application Deployment

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = Applicable, ResolvedState = Installed</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]

# Requirement Rules Not Met

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = NotApplicable, ResolvedState = None</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]
</code></pre>

I logg posten ovan indikerar det **aktuella läget** om programmet är installerat på enheten. **Tillämplighets** anger om programmet är tillämpligt baserat på definierade krav regler. **ResolvedState** anger det önskade tillstånd för programmet baserat på distributions syftet.

> [!TIP]
> Använd [verktyget för distributions övervakning](../../core/support/deployment-monitoring-tool.md) för att visa program tillstånd, tillämplighets tillstånd och krav överträdelser.

## <a name="next-steps"></a>Nästa steg

- [Hämtning av program](deployment-download-technical-reference.md)
