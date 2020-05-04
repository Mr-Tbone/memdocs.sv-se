---
title: Teknisk referens för program distribution av klient komponenter
titleSuffix: Configuration Manager
description: Klient komponenter som används för att felsöka program distribution i Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 701a3456-9dd6-4aaa-9c5a-37c1e1773216
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 35b54bd5868197d607a15ab1d4759d03968b9892
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709805"
---
# <a name="understanding-application-deployment-client-components"></a>Förstå klient komponenter för program distribution

*Gäller för: Configuration Manager (aktuell gren)*

Utvärderings-och tvångs åtgärder för program distribution hanteras av DCM-agenten och CI agent-komponenterna på klienten. Den här artikeln förklarar hur ett typiskt DCM-och CI Agent-jobb fungerar.

## <a name="dcm-agent"></a>DCM-agent

DCM-agenten är den klient komponent på hög nivå som ansvarar för utvärdering av konfigurations objekt, vilket omfattar program. När en distribution aktive ras eller tillämpas, skapas ett DCM Agent jobb som läser tilldelnings principen och avgör vilka åtgärder som måste utföras. Den här aktiviteten kan spåras i **DCMAgent. log** på klienten med hjälp av jobb-ID: t för DCM-agenten som du kan identifiera genom att söka efter programmets unika ID.

### <a name="device-deployments"></a>Enhets distributioner

- För **nödvändiga** distributioner visar DCMAgent. log lämpliga åtgärder. Dessa åtgärder kan variera beroende på om distributionens tids gräns redan har passerats.

    ```text
    # Evaluation Job example:
    DCMAgentJob({A9E850E2-91B0-4122-94FD-D14EDF925AF7}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/RequiredApplication_fc76ef0a-3ab0-4110-8cce-1addc36d0225 version:3 with actions: Evaluation, Content Download

    # Enforcement Job example:
    DCMAgentJob({4C8A9F6E-390B-450E-B505-B5698DB68EDD}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/RequiredApplication_fc76ef0a-3ab0-4110-8cce-1addc36d0225 version:3 with actions: Evaluation, Install, Uninstall, Update, Look-ahead Install, Look-ahead Uninstall, Look-ahead Update
    ```

- För **tillgängliga** distributioner visar DCMAgent. log att distributionen `is not mandatory`. För dessa distributioner utförs program utvärdering, men tvång ignoreras om användaren inte har initierat installationen.

    ```text
    # Evaluation Job example:
    DCMAgentJob({E353BF94-D7ED-4ADD-AF0F-9273F6A67FC1}): CDCMAgentJob::PopulateCIsFromAssignment - [SCAN] CI policy Id :ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/RequiredApplication_fc76ef0a-3ab0-4110-8cce-1addc36d0225 version:3 - Assignment:{3AC57DFE-3F87-4C59-930B-B9F57CB41B91} is not mandatory.

    # Enforcement Job (user initiated) example:
    Request to enforce application ConfigMgr Toolkit(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/Application_fc76ef0a-3ab0-4110-8cce-1addc36d0225.3) immediately for target: machine with action(s): Evaluation, Install, Update
    CDCMAgentJobMgr::CreateInteractiveJob - Queuing new job: {D331249E-F7DE-481B-A497-8E8B5E7B91C3}

    ```

### <a name="user-deployments"></a>Användar distributioner

- För **nödvändiga** distributioner visar DCMAgent. log lämpliga åtgärder. Dessa åtgärder kan variera beroende på om distributionens tids gräns redan har passerats.

    ```text
    # Evaluation Job example:
    DCMAgentJob({65D9688D-1781-4DA3-B07A-193D481251C6}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98 version:2 with actions: Evaluation, Content Download

    # Enforcement Job example:
    DCMAgentJob({2B0DA272-FC65-4F31-9557-C4D840D650F1}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98 version:2 with actions: Evaluation, Install, Uninstall, Update, Look-ahead Install, Look-ahead Uninstall, Look-ahead Update
    ```

- För **tillgängliga** distributioner skapas DCM Agent-jobb för utvärdering och tvång när programinstallationen initieras av användaren.

    ```text
    # Evaluation Job example:
    DCMAgentJob({FBB44C84-DB06-41F7-8DC1-D9BA368F0C20}): CDCMAgentJob::PopulateCIsFromAssignment - [SCAN] CI policy Id :ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98 version:2 - Assignment:{7EA17128-EB4F-448A-88A7-B865E7DA228C} is not mandatory.

    # Enforcement Job example:
    CAppMgmtSDK::EnforceAppPolicy ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98.
    CDCMAgentJobMgr::CreateInteractiveJob - Queuing new job: {7936D7F3-24B0-401D-BADD-59EB5B49C2C2}
    ```

## <a name="ci-agent"></a>CI-agent

CI agent är klient komponenten som ansvarar för utvärdering och reparation av konfigurations objekt. DCM-agenten läser tilldelnings principen och skapar ett jobb för CI Agent-komponenten för att utföra de begärda åtgärderna. **DCMAgent. log** registrerar CI Agent jobb-ID, vilket är användbart för att spåra CI agent-aktiviteten i **CIAgent. log** på klienten.

<pre><code class="lang-text">DCMAgentJob({E353BF94-D7ED-4ADD-AF0F-9273F6A67FC1}): CDCMAgent::InitiateCIAgentJob - <b>Starting CI Agent Job</b> {57AF6FA1-3482-4469-9881-A63F41D18406} for target: machine. Refer to this CI agent job ID in ciagent.log for more details
</code></pre>

Ett typiskt CI Agent-jobb går igenom flera faser, som kan identifieras genom filtrering av **CIAgent. log** på jobb-ID: t för CI agent `TransitionState`och letar efter. Några av huvud faserna för ett jobb för program distribution av CI-agenten är:

- **DownloadingCIs**
  - Under den här fasen hämtas programmetadata som krävs för att utvärdera programmet. Metadata innehåller identifierings metod, krav regler, globala villkor osv. Den här aktiviteten kan spåras i **CIDownloader. log** och **DataTransferService. log**. För **tillgängliga** distributioner sker den här processen under den första utvärderingen av programmet. För **nödvändiga** distributioner sker dock den här processen omedelbart efter att principen har hämtats.

- **InvokingSdmMethod**
  - Under den här fasen används identifierings metoden för programmet för att kontrol lera om programmet är installerat och det önskade läget bestäms. Den här aktiviteten kan spåras i **AppDiscovery. log** och **AppIntentEval. log**. Mer information om den här fasen finns i [program utvärdering](deployment-evaluation-technical-reference.md).

- **StateDownloadingContents**
  - Under den här fasen hämtas program innehållet om det behövs. Den här aktiviteten kan spåras i **CAS. log**, **ContentTransferManager. log**, **filen LocationServices. log**och **DataTransferService. log**. Mer information om den här fasen finns i [program hämtning](deployment-download-technical-reference.md).

- **StateEnforcingCIs**
  - Under den här fasen initieras programinstallationen. Den här aktiviteten kan spåras i **AppEnforce. log**. Mer information om den här fasen finns i [program installation](deployment-install-technical-reference.md).

- **StateEnforcementReporting**
  - Under den här fasen registreras programmets installations tillstånd för rapportering till hanterings platsen. Den här aktiviteten kan spåras i **StateMessage. log**.

Även om CI Agent-jobbet går igenom alla faser, hoppar det över fasen om det inte behövs. Exempel: för **tillgängliga** distributioner StateDownloadingContents-och StateEnforcingCIs-faser hoppas över tills användaren försöker installera programmet från Software Center. För **obligatoriska** distributioner hämtar dock StateDownloadingContents-fasen program innehåll (om det behövs) när tilldelningen aktive ras, men StateEnforcingCIs-fasen hoppas över om tids gränsen är i framtiden. Det här beteendet kan observeras i CIAgent. log genom filtrering av CI Agent jobb-ID och letar `Skipping policy`efter.

```text
{57AF6FA1-3482-4469-9881-A63F41D18406} - Skipping policy CI <CI Unique ID> and all dependents for ContentDownload task since CI action was not requested.
{57AF6FA1-3482-4469-9881-A63F41D18406} - Skipping policy CI <CI Unique ID> and all dependents for Enforce task since CI action was not requested.
```

## <a name="next-steps"></a>Nästa steg

- [Program utvärdering](deployment-evaluation-technical-reference.md)
- [Hämtning av program](deployment-download-technical-reference.md)
- [Programinstallation](deployment-install-technical-reference.md)
