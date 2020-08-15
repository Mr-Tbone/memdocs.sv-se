---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 08/14/2020
ms.openlocfilehash: 13a5b771f712420939f87073854faab3c38270c9
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252480"
---
<!--Don't apply H2 in this include file since they are context driven by article-->

### <a name="when-the-sms-provider-is-remote-from-the-cas-you-may-encounter-an-internal-server-error-from-the-admin-console"></a><a name="bkmk_dblhop"></a> När SMS-providern är fjärran sluten till certifikat utfärdarna kan du stöta på ett internt Server fel från administratörs konsolen

**Fel meddelande:** Lokal felkod: 500 internt Server fel

**Scenario 1:** När du kör Configuration Manager version 2002 och det finns en fjärran sluten Provider för certifikat utfärdarna kan du stöta på ett internt Server fel från administratörs konsolen.

**Scenario 2:** När du kör Configuration Manager version 2006 kan du också stöta på det här felet om tjänst anslutnings punkten inte kan ansluta till providern på den primära platsen och återgår till providern för certifikat utfärdarna. 

**Scenario 3:** Om CAS har uppgraderats till version 2006 men den primära servern inte har uppgraderats än, kommer begäran att dirigeras via CAS-providern. Om providern är fjärran sluten kan du stöta på ett internt Server fel från administratörs konsolen. 

**Lösning:** Följ anvisningarna för [CAS](../../core/servers/manage/cmpivot-changes.md#cas-has-a-remote-provider) i CMPivot-artikeln för att undvika det här scenariot med dubbla hopp.

### <a name="when-multi-factor-authentication-is-enabled-most-tenant-attach-features-dont-work"></a><a name="bkmk_mfa"></a> När Multi-Factor Authentication har Aktiver ATS fungerar inte de flesta klient kopplings funktioner
<!--7986450, 7988266-->
**Scenario:** Om [SMS-providern](../../core/plan-design/hierarchy/plan-for-the-sms-provider.md) som kommunicerar med [tjänst anslutnings punkten](../../core/servers/deploy/configure/about-the-service-connection-point.md) har kon figurer ATS för att använda Multi-Factor Authentication kan du inte installera program, köra CMPivot-frågor och utföra andra åtgärder från administratörs konsolen. Du får felkod 403, förbjudet.  

**Lösning:** Den aktuella lösningen är att konfigurera hierarkin till standard verifierings nivån för **Windows-autentisering**. Mer information finns i [avsnittet Authentication (autentisering) i SMS-provider artikeln](../../core/plan-design/hierarchy/plan-for-the-sms-provider.md#bkmk_auth).

