---
title: Felsöka anslutnings- och enhetsåtgärder för klientorganisation
titleSuffix: Configuration Manager
description: Felsöka klient anslutnings-och enhets åtgärder för Configuration Manager
ms.date: 08/11/2020
ms.topic: troubleshooting
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 44c2eb8a-3ccc-471f-838b-55d7971bb79e
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 6dfe7bb44a70d26a68c6d3743ecdb05e5d55e3f1
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129329"
---
# <a name="troubleshooting-tenant-attach-and-device-actions"></a>Felsöka klient kopplings-och enhets åtgärder

*Gäller för: Configuration Manager (aktuell gren)*

Från och med Configuration Manager 2002 kan Configuration Manager-klienter synkroniseras med administrations Center för Microsoft Endpoint Manager. Vissa klient åtgärder kan köras från administrations Center för Microsoft Endpoint Manager på de synkroniserade klienterna.

Tillgängliga åtgärder är:
- Synkronisera enhetsprincip
- Synkronisera användarprincip
- Apputvärderingscykel


[![Enhets översikt i administrations Center för Microsoft Endpoint Manager](./media/3555758-device-overview-actions.png)](./media/3555758-device-overview-actions.png#lightbox)
  
När en administratör kör en åtgärd från administrations centret för Microsoft Endpoint Manager vidarebefordras meddelande förfrågan till Configuration Manager plats och från platsen till klienten.

## <a name="log-files"></a>Loggfiler

Använd följande loggar som finns på tjänst anslutnings punkten:

- **CMGatewaySyncUploadWorker. log**
- **CMGatewayNotificationWorker. log**

Använd följande loggar som finns på hanterings platsen:

- **BgbServer. log**

Använd följande loggar som finns på klienten:

- **CcmNotificationAgent.log**

## <a name="review-your-upload"></a><a name="bkmk_review"></a>Granska din uppladdning

1. Öppna **CMGatewaySyncUploadWorker. log** från &lt; installations katalogen för ConfigMgr> \Loggar.
1. Nästa synkroniseringstid anges av logg poster som liknar `Next run time will be at approximately: 02/28/2020 16:35:31` .
1. Sök efter logg poster som liknar för enhets uppladdningar `Batching N records` . **N** är antalet ändrade enheter som har överförts sedan den senaste överföringen.
1. Uppladdningen sker var 15: e minut för ändringar. När ändringarna har laddats upp kan det ta ytterligare 5 till 10 minuter innan klient ändringarna visas i **administrations centret för Microsoft Endpoint Manager**.


## <a name="configuration-manager-components-and-log-flow"></a>Configuration Manager-komponenter och logg flöde

- **SMS_SERVICE_CONNECTOR**: använder Gateway Notification Worker för att bearbeta meddelandet från administrations Center för Microsoft Endpoint Manager.
- **SMS_NOTIFICATION_SERVER**: hämtar meddelandet och skapar ett klient meddelande.
- **BgbAgent**: klienten hämtar uppgiften och kör den begärda åtgärden.

### <a name="sms_service_connector"></a>SMS_SERVICE_CONNECTOR

När en åtgärd initieras från administrations centret för Microsoft Endpoint Manager, bearbetar **CMGatewayNotificationWorker. log** begäran.  

```text
Received new notification. Validating basic notification details...
Validating device action message content...
Authorized to perform client action. TemplateID: RequestMachinePolicy TenantId: a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2 AADUserID:     a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2
Forwarded BGB remote task. TemplateID: 1 TaskGuid: a43dd1b3-a006-4604-b012-5529380b3b6f TaskParam: TargetDeviceIDs: 1  
```
 
1. Ett meddelande tas emot från administrations Center för Microsoft Endpoint Manager.

   ```text
   Received new notification. Validating basic notification details..
   ```

1. Användar-och enhets åtgärder verifieras.

   ```text
   Validating device action message content... 
   Authorized to perform client action. TemplateID: RequestMachinePolicy TenantId: a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2 AADUserID:     a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2
   ```

1. Fjärruppgiften vidarebefordras till SMS_NOTIFICATION_SERVER.

    ```text
   Forwarded BGB remote task. TemplateID: 1 TaskGuid: a43dd1b3-a006-4604-b012-5529380b3b6f TaskParam: TargetDeviceIDs: 1  
    ```


### <a name="sms_notification_server"></a>SMS_NOTIFICATION_SERVER

När meddelandet har skickats till SMS_NOTIFICATION_SERVER skickas en uppgift från hanterings platsen till motsvarande klient. Du ser följande i **BgbServer. log**, som finns på hanterings platsen:

```text
Get one push message from database.
Starting to send push task (PushID: 7 TaskID: 8 TaskGUID: A43DD1B3-A006-4604-B012-5529380B3B6F TaskType: 1 TaskParam: ) to 1 clients  with throttling (strategy: 1 param: 42)
```

### <a name="bgbagent"></a>BgbAgent

Det sista steget inträffar på klienten och kan visas i **CcmNotificationAgent. log**. När uppgiften tas emot begär Schemaläggaren att utföra åtgärden. När åtgärden utförs visas ett bekräftelse meddelande:

```text
Receive task from server with pushid=7, taskid=8, taskguid=A43DD1B3-A006-4604-B012-5529380B3B6F, tasktype=1 and taskParam=

Send Task response message <BgbResponseMessage TimeStamp="2020-01-21T15:43:43Z"><PushID>8</PushID><TaskID>9</TaskID><ReturnCode>1</ReturnCode></BgbResponseMessage> successfully.
```

## <a name="common-issues"></a>Vanliga problem

### <a name="unauthorized-to-perform-client-action"></a><a name="bkmk_noauth"></a>Saknar behörighet att utföra klient åtgärder

Om administratören inte har de behörigheter som krävs i Configuration Manager, ser du ett `Unauthorized` svar i **CMGatewayNotificationWorker. log**.

```text
Received new notification. Validating basic notification details..
Validating device action message content...
Unauthorized to perform client action. TemplateID: RequestMachinePolicy TenantId: a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2 AADUserID: 3a1e89e6-e190-4615-9d38-a208b0eb1c78
```  

Se till att användaren som kör åtgärden från administrations centret för Microsoft Endpoint Manager har de behörigheter som krävs på Configuration Manager-platsen. Mer information finns i [Microsoft Endpoint Manager-klient anslutning för krav](device-sync-actions.md#prerequisites).

## <a name="known-issues"></a>Kända problem

### <a name="specific-devices-dont-synchronize"></a>Vissa enheter synkroniseras inte

<!--7099564-->
Det är möjligt att vissa enheter, som är Configuration Manager klienter, inte överförs till tjänsten.

**Påverkade enheter:** Om en enhet är en distributions plats som använder samma PKI-certifikat för både distributions plats funktionerna och dess klient agent, kommer enheten inte att tas med i synkroniseringen av klient anslutningens enhet.

**Beteende:** När du utför en klient anslutning under den här fasen utförs en fullständig synkronisering första gången. Efterföljande synkroniseringsförsök är delta i synkroniseringar. Eventuella uppdateringar av de påverkade enheterna gör att enheten tas bort från synkroniseringen.


## <a name="next-steps"></a>Nästa steg

[Felsöka klient information](troubleshoot-client-details.md) 
 för ConfigMgr [Aktivera samhantering](../comanage/overview.md) för att få fler moln drivna funktioner som villkorlig åtkomst.
