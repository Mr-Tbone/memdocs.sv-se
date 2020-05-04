---
title: Teknisk referens för program nedladdning
titleSuffix: Configuration Manager
description: Felsöka teknisk referens för program hämtning för Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 41c29a07-9bf6-4ec4-b3f2-1c05e001eff7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: effa8115a5023a8e0611f6bc4245a101b3a47e38
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709812"
---
# <a name="application-download-in-configuration-manager"></a>Hämtning av program i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Innan du fortsätter kan du granska [program distributionens klient komponenter](client-components-technical-reference.md) för att förstå jobb bearbetning av DCM-och CI-agenten.

## <a name="download-initiation"></a>Hämta initiering

Hämtning av program innehåll initieras av CI Agent-komponenten på klienten under **StateDownloadingContents** -fasen. Den här processen är densamma oavsett om programmet distribueras till en enhets samling eller en användar samling.

- För **tillgängliga** distributioner hämtas program innehållet när användaren initierar programinstallationen från Software Center.
- För **obligatoriska** distributioner laddas program innehållet ned när tilldelningen aktive ras och programmet hittas efter utvärderingen. Information om hur du aktiverar tilldelningen finns i artikeln [program distribution till enhets samlingar](device-deployment-technical-reference.md) eller [program distribution till användar samlingar](user-deployment-technical-reference.md) .

När CI-agenten startar innehålls hämtningen skapas en aktivitet som hanteras av komponenten CI Task Manager. CI Task Manager initierar sedan innehålls hämtningen. Den här aktiviteten kan spåras i **CITaskMgr. log** med hjälp av ett unikt ID för distributions typen.

<pre><code class="lang-text"><b>Initiating task ContentDownload</b> for CI ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2 (ConfigMgr Toolkit - Windows Installer (*.msi file)) for target: , consumer: {53EA65C2-D596-4215-83E4-F7007B78E18C}
</code></pre>

## <a name="distribution-point-location"></a>Plats för distributions plats

Alla hämtnings aktiviteter hanteras av komponenten för innehålls åtkomst, som ansvarar för att hantera-klientens cacheminne. När hämtnings aktiviteten har skapats kontrollerar komponenten för innehålls åtkomst om innehållet redan är tillgängligt i klientens cacheminne. Om innehållet inte är tillgängligt skapas en plats förfrågan för att hämta en lista över distributions platser där innehållet kan hämtas. Den här aktiviteten kan spåras i **ca. log** och **filen LocationServices. log** på klienten med hjälp av unikt innehålls-id.

```text
Requesting locations synchronously for content Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1 with priority Foreground
ContentLocationRequest : <Request XML Body>
Reply Message Body : <Reply XML Body>
```

> [!IMPORTANT]
> Även om plats tjänst komponenten hanterar plats begär Anden begär den inte direkt platser från hanterings platsen. Alla begär anden till hanterings platsen går vanligt vis igenom CCM-meddelande komponenten, som loggar in på **CcmMessaging. log**.

Platsens svars-XML innehåller listan över distributions platser baserade på klientens gränser grupp. Den här listan parsas och sparas i WMI på klienten enligt [prioriteten för innehålls källan](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#content-source-priority). Den här aktiviteten kan visas i **ContentTransferManager. log**med hjälp av unikt innehålls-id och letar efter `Persisted location`. 

Om platsens svars-XML inte innehåller några distributions platser visas `Received empty location update` **ContentTransferManager. log** och klienten kan fastna på 0% när programmet laddas ned. Detta svar kan vanligt vis inträffa på grund av problem med konfiguration av gränser. Mer information finns i [hämtnings problem](../deploy-use/troubleshoot-application-deployment.md#download-failures).

## <a name="content-download"></a>Hämta innehåll

När distributions platsens platser har hämtats skapar komponenten för innehålls åtkomst ett innehålls överförings jobb. Den här aktiviteten kan spåras i **ca. log** med unikt innehålls-id.

<pre><code class="lang-text">Submitted CTM job <b>{6D0EA720-EB4E-4893-8395-8B27470A6CFB}</b> to download Content <b>Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1</b> under context System
</code></pre>

Innehålls överförings hanteraren skapar sedan ett Dataöverföring tjänst jobb för att hämta innehållet. Den här aktiviteten kan spåras i **ContentTransferManager. log** på klienten med hjälp av unikt innehålls-id.

<pre><code class="lang-text">CTM job <b>{6D0EA720-EB4E-4893-8395-8B27470A6CFB}</b> (corresponding DTS job <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b>) started download from '<Distribution Point URL>/<b>Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1</b>' for full content download.
</code></pre>

> [!NOTE]
> Den här logg posten kan användas för att identifiera CTM och DTS-jobbets ID, som kan användas för att spåra förloppet för innehålls överföringen i **ContentTransferManager. log** respektive **DataTransferService. log** .

Dataöverföring tjänsten utför nedladdningen av program innehållet genom att skapa ett Background Intelligent Transfer Service-jobb (BITS) och väntar på att nedladdningen ska slutföras. Den här aktiviteten kan spåras i **DataTransferService. log** på klienten med hjälp av det DTS-jobb-ID som hämtats från **ContentTransferService. log**.

<pre><code class="lang-text">Starting BITS job '{40263E01-2EDD-462F-ABBA-A5E892CB9229}' for DTS job '<b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b>' under user 'S-1-5-18'.
DTSJob <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b> in state 'DownloadingData'.
DTS job <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b> has completed
</code></pre>

När hämtningen är klar meddelas komponenten för innehålls åtkomst. Komponenten för innehålls åtkomst verifierar sedan det hämtade innehållet för att säkerställa att innehållet inte har ändrats under nedladdningen. Den här aktiviteten kan spåras i **ca. log** med unikt innehålls-id.

```text
Hash verification succeeded for content Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1 downloaded under context System
```

Slutligen, efter att innehållet har verifierats, tar CI-agenten emot meddelandet slutförd uppgift och CI Agent-jobbet flyttas till nästa fas.

<pre><code class="lang-text">CIAgentJob({2BF84225-C9E8-49A6-A308-A160C4B799D3}): CAgentJob::HandleEvent(<b>Event=CITaskComplete, CurrentState=StateDownloadingContents</b>)
</code></pre>

## <a name="next-steps"></a>Nästa steg

- [Programinstallation](deployment-install-technical-reference.md)
