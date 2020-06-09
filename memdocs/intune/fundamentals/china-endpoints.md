---
title: Nätverksslutpunkter för kinesiska distributioner – Microsoft Intune
titleSuffix: ''
description: Granska kinesiska slutpunkter för Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/28/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: kerimh
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: b5551e537716ed12a0a5b5de19b747ffc7c4dcac
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347346"
---
# <a name="china-endpoints-for-microsoft-intune"></a>Kinesiska slutpunkter för Microsoft Intune

På den här sidan visas en lista över kinesiska slutpunkter om krävs för proxyinställningarna i dina Intune-distributioner.

Om du vill hantera enheter bakom brandväggar och proxyservrar, måste du aktivera kommunikation för Intune.

- Proxyservern måste ha stöd för både **HTTP (80)** och **HTTPS (443)** eftersom Intune-klienter använder båda protokollen
- För vissa åtgärder (t.ex. nedladdning av programuppdateringar) kräver Intune att det finns en oautentiserad åtkomst till proxyservern för att få åtkomst till manage.microsoft.com

Du kan ändra inställningarna för proxyservern på enskilda klientdatorer. Du kan också använda grupprincipinställningar till att ändra inställningarna för alla klientdatorer som finns bakom en angiven proxyserver.

Hanterade enheter kräver konfigurationer som låter **Alla användare** komma åt tjänster genom brandväggar.

Mer information om automatisk registrering av Windows 10 och enhetsregistrering för kinesiska kunder finns i [Konfigurera registrering för Windows-enheter](../enrollment/windows-enroll.md#windows-10-auto-enrollment-and-device-registration).

I följande tabeller visas de portar och tjänster som Intune-klienten har åtkomst till:

|**Slutpunkt**|**IP-adress**|
|---------------------|-----------|
|*.manage.microsoft.cn | 40.73.38.143<br>139.217.97.81<br>52.130.80.24<br>40.73.41.162<br>40.73.58.153<br>139.217.95.85 |


## <a name="intune-customer-designated-endpoints-in-china"></a>Slutpunkter som tilldelas Intune-kunder i Kina
- Azure Portal: https:\//portal.azure.cn/
- Office 365: https:\//portal.partner.microsoftonline.cn/
- Intune-företagsportal: https:\//portal.manage.microsoftonline.cn/
- Administrationscenter för Microsoft Endpoint Manager: https:\//endpoint.microsoftonline.cn/


## <a name="partner-service-endpoints"></a>Partnertjänstslutpunkter

Intune som, drivs av 21Vianet, är beroende av följande partnertjänstslutpunkter:
- Azure AD Sync-tjänsten: https:\//syncservice.partner.microsoftonline.cn/DirectoryService.svc
- Evo STS: https:\//login.chinacloudapi.cn/
- Azure AD Graph: https:\//graph.chinacloudapi.us
- MS Graph: https:\//microsoftgraph.chinacloudapi.cn
- ADRS: https:\//enterpriseregistration.partner.microsoftonline.cn

[!INCLUDE [Intune notices](../includes/windows-push-notification-services.md)]

[!INCLUDE [Intune notices](../includes/apple-device-network-information.md)]

## <a name="next-steps"></a>Nästa steg
[Läse mer om Intune, som drivs av 21Vianet, i Kina](china.md)

