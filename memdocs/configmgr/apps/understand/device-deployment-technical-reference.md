---
title: Teknisk referens för app-distribution till enhets samlingar
titleSuffix: Configuration Manager
description: Felsöka program distributioner till teknisk referens för enhets samlingar för Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 4e62b04d-fe56-42ed-87dc-e673cf061d52
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1965029a1933793057dc5768bacb391afd645404
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709763"
---
# <a name="application-deployment-for-device-collections"></a>Program distribution för enhets samlingar

*Gäller för: Configuration Manager (aktuell gren)*

När ett program distribueras till en enhets samling är principen riktad till alla enheter i samlingen, oavsett distributions syfte. I den här artikeln beskrivs hämtning och distribution av principer på klienten.

> [!TIP]
> All information som behövs för att granska klient loggarna kan erhållas genom att köra SQL-frågan som refereras i avsnittet [innan du börjar](app-deployment-technical-reference.md#before-you-begin) .

## <a name="policy-download"></a>Hämta princip

När principen för program distributionen är riktad mot klienten laddar klienten ned principen vid nästa princip avsöknings cykel. När klienten laddar ned principen hämtas relaterade principer utöver distributions principen. Dessa relaterade principer omfattar principen för programmet, distributions typ, globala villkor osv. Princip hämtnings aktivitet kan spåras i **Policy Agent. log** på klienten med hjälp av ett unikt ID för programmet eller tilldelningen.

<pre><code class="lang-text">Download of policy CCM_Policy_Policy5.PolicyID="{<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>}",PolicySource="SMS:PS1",PolicyVersion="1.00" completed (DTS Job ID: {AE88E639-0E59-40D7-AAA9-4403AAE6EE82})
Policy state for [CCM_Policy_Policy5.PolicyID="{<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>}",PolicySource="SMS:PS1",PolicyVersion="1.00"] is currently [Active]
</code></pre>

När principerna har hämtats på klienten skapar Scheduler-komponenten scheman för aktivering och tillämpning av distribution.

## <a name="deployment-activation"></a>Distributions aktivering

Program utvärdering initieras när distributionen aktive ras. Scheduler-komponenten skapar ett schema för att aktivera tilldelningen vid den tillgängliga tiden som kon figurer ATS i distributionen. Den här aktiviteten kan spåras i **Scheduler. log** på klienten med hjälp av unikt ID för program tilldelning.

- För **obligatoriska** distributioner skapas aktiverings schema, men har en fördröjning på upp till två timmar för att undvika resurs konkurrens på plats servrar och distributions platser. Fördröjningen bidrar till att undvika konkurrens eftersom program innehåll kan hämtas under utvärderingen om programmet är tillämpligt baserat på definierade krav regler.

    <pre><code class="lang-text">SMSTrigger '15AF8C4000080000' for scheduler '<b>Machine/{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' will fire at 08/15/2019 01:44:00 PM with randomization.
    </code></pre>

- För **tillgängliga** distributioner skapas aktiverings schema för att stängas av vid den tillgängliga tiden som kon figurer ATS i distributionen.

    <pre><code class="lang-text">SMSTrigger '1E4F8C4000080001' for scheduler '<b>Machine/{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</b>' will fire at 08/15/2019 01:13:33 PM without randomization.
    </code></pre>

När schema tiden anländer skickar Scheduler-komponenten aktiverings meddelandet till DCM-agenten för att utföra program utvärderingen.

<pre><code class="lang-text">Sending message for schedule '<b>Machine/{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</b>' (Target: 'direct:DCMAgent', Name: '')
</code></pre>

DCM-agenten tar emot aktiverings meddelandet och skapar ett jobb för att utvärdera programmet.

```text
CDCMAgent::HandleMessage - Message received for machine: '<?xml version='1.0' ?><CIAssignmentMessage MessageType='Activation'><AssignmentID>{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</AssignmentID></CIAssignmentMessage>'
```

## <a name="deployment-enforcement"></a>Tvingande distribution

Programinstallationen initieras när distributionen tillämpas.

- För **obligatoriska** distributioner skapar Scheduler ett schema för tids gräns efter att principen har laddats ned för att genomdriva programmet vid distributionens tids gräns. Schemat för tids gräns är inte slumpmässigt som standard. Slumpmässigt beteende för aktivering kan kontrol leras av klient inställningen [inaktivera tids gräns för slumpmässig tids gräns](../../core/clients/deploy/about-client-settings.md#disable-deadline-randomization) .

    <pre><code class="lang-text">SMSTrigger '15EF8C4000080000' for scheduler '<b>Machine/DEADLINE:{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' will fire at 08/15/2019 03:05:00 PM without randomization.
    </code></pre>

    Vid tids gränsen skickar Scheduler-komponenten meddelandets tids gräns till DCM-agenten. 

    <pre><code class="lang-text">Sending message for schedule '<b>Machine/DEADLINE:{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' (Target: 'direct:DCMAgent', Name: '')
    </code></pre>

    DCM-agenten tar emot tids gräns meddelandet och skapar ett jobb för att genomdriva programmet.
  
    ```text
    CDCMAgent::HandleMessage - Message received for machine: '<?xml version='1.0' ?><CIAssignmentMessage MessageType='EnforcementDeadline'><AssignmentID>{5F2FA409-C9B2-4100-8BC8-051820311DE1}</AssignmentID></CIAssignmentMessage>'
    ```

    > [!NOTE]
    > För distributioner med deadline tidigare aktive ras programmet och verkställs omedelbart av samma DCM Agent-jobb som utför utvärderings-, hämtnings-och installations åtgärder.

- För **tillgängliga** distributioner finns det inget tids gräns schema eftersom tvången inträffar när programinstallationen initieras av användaren från Software Center. När användaren startar en installation skapas ett DCM-Agent jobb för att utföra program utvärdering, hämtning och installation. Den här aktiviteten kan spåras i **DCMAgent. log** på klienten.

## <a name="next-steps"></a>Nästa steg

- [Förstå klient komponenter för program distribution](client-components-technical-reference.md)
