---
title: Nätverksslutpunkter för amerikanska myndigheters distributioner – Microsoft Intune
titleSuffix: ''
description: Granska slutpunkter för amerikanska myndigheter för Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/30/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5f6682cb-5fcd-4018-b7f7-71768ad3152e
ms.reviewer: kerimh
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: d1574e07ca58debaef5bbc134a86d76aa21778a3
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347274"
---
# <a name="us-government-endpoints-for-microsoft-intune"></a>Slutpunkter för amerikanska myndigheter för Microsoft Intune

På den här sidan visas en lista över slutpunkter för myndigheter i USA som krävs för proxyinställningarna i dina Intune-distributioner.

Om du vill hantera enheter bakom brandväggar och proxyservrar, måste du aktivera kommunikation för Intune.

- Proxyservern måste ha stöd för både **HTTP (80)** och **HTTPS (443)** eftersom Intune-klienter använder båda protokollen
- För vissa åtgärder (t.ex. nedladdning av programuppdateringar) kräver Intune att det finns en oautentiserad åtkomst till proxyservern för att få åtkomst till manage.microsoft.com

Du kan ändra inställningarna för proxyservern på enskilda klientdatorer. Du kan också använda grupprincipinställningar till att ändra inställningarna för alla klientdatorer som finns bakom en angiven proxyserver.

Hanterade enheter kräver konfigurationer som låter **Alla användare** komma åt tjänster genom brandväggar.

För ytterligare information om automatisk registrering av Windows 10 och enhetsregistrering för amerikanska myndighetskunder, se [Konfigurera registrering för Windows-enheter](../enrollment/windows-enroll.md#windows-10-auto-enrollment-and-device-registration).

I följande tabeller visas de portar och tjänster som Intune-klienten har åtkomst till:

|**Slutpunkt**|**IP-adress**|
|---------------------|-----------|
|*. manage.microsoft.us | 52.243.26.209 <br> 52.247.173.11 <br> 52.227.183.12 <br>52.227.180.205 <br> 52.227.178.107 <br> 13.72.185.168 <br> 52.227.173.179 <br> 52.227.175.242 <br> 13.72.39.209 <br> 52.243.26.209 <br> 52.247.173.11 |
| enterpriseregistration.microsoftonline.us | 13.72.188.239 <br> 13.72.55.179 |

## <a name="us-government-customer-designated-endpoints"></a>Slutpunkter som tilldelas amerikanska myndighetskunder:
- Azure-portalen: https:\//portal.azure.us/ 
- Office 365: https:\//portal.office365.us/ 
- Intune-företagsportalen: https:\//portal.manage.microsoft.us/ 
- Administrationscenter för Microsoft Endpoint Manager: https:\//endpoint.microsoft.us/

## <a name="partner-service-endpoints-that-intune-depends-on"></a>Partnertjänstslutpunkter som Intune är beroende av:
- AAD Sync Service: https:\//syncservice.gov.us.microsoftonline.com/DirectoryService.svc
- Evo STS: https:\//login.microsoftonline.us
- Directory Proxy: https:\//directoryproxy.microsoftazure.us/DirectoryProxy.svc
- AAD Graph: https:\//directory.microsoftazure.us and https:\//graph.microsoftazure.us
- MS Graph: https:\//graph.microsoft.us
- ADRS: https:\//enterpriseregistration.microsoftonline.us

[!INCLUDE [Intune notices](../includes/windows-push-notification-services.md)]

[!INCLUDE [Intune notices](../includes/apple-device-network-information.md)]

## <a name="next-steps"></a>Nästa steg
[Nätverksslutpunkter för Microsoft Intune](intune-endpoints.md)

