---
title: Arbetsflöde för Azure AD-autentisering
titleSuffix: Configuration Manager
description: Information om installations processen för Configuration Manager-klienten på en Windows 10-enhet med Azure Active Directory autentisering
ms.date: 07/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9aaf466a-3f40-4468-b3cd-f0010f21f05a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9215688104b1a929cad7c172126387961851760b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714124"
---
# <a name="azure-ad-authentication-workflow"></a>Arbetsflöde för Azure AD-autentisering

*Gäller för: Configuration Manager (aktuell gren)*

Den här artikeln är en teknisk referens för Configuration Manager klient installations processen på en Windows 10-enhet som är ansluten till Azure Active Directory (Azure AD). Den innehåller information om arbets flödes processen för enhetsautentisering och klient installation.  
 

## <a name="azure-ad-token-request-workflow"></a>Arbets flöde för Azure AD-Tokenbegäran

![Arbets flödes diagram för Azure AD CCMSetup](media/azure-ad-install-workflow.png)  

### <a name="1-azure-ad-token-request"></a>1. begäran om Azure AD-token

En domänansluten Windows 10 Azure AD-klient använder Azure AD-parametrar för att begära en token. Följande poster loggas i **CCMSetup. log**:

- Begär Azure AD-enhets-token:

    ``` Log
    Getting AAD (device) token with: ClientId = 22ed38d9-XXXX-4036-XXXX-a98452fda4fc, ResourceUrl = https://ConfigMgrService, AccountId = https://login.microsoftonline.com/common/oauth2/token
    ```

- Om den inte kan hämta en enhets-token begär den en Azure AD-användartoken:

    ``` Log
    Getting AAD (user) token with: ClientId = f1f9b14e-XXXX-4f17-XXXX-2593f6eee91e, ResourceUrl = https://ConfigMgrService, AccountId = X49FC29A-ECE3-XXX-A3C1-XXXXXXF035A6E
    ```

> [!NOTE]
> En klient ska få ett WPJ-certifikat (Workplace Join) när den ansluter till Azure AD. Om ett certifikat för en arbets plats anslutning inte hittas försöker klienten inte att skapa begäran med hjälp av kommunikations kanalen för säkerhetstokentjänsten (CCM_STS). Det här problemet beror på att klienten inte kan lägga till en Azure AD-token i begäran. Enheten har vanligt vis inte det här certifikatet när klienten inte är korrekt ansluten till Azure AD.
>
> Om token inte är giltig vidarebefordrar inte heller CMG (Cloud Management Gateway) begäran till de interna plats rollerna. Token kan vara ogiltig om klienten inte är registrerad som en moln hanterings tjänst i Configuration Manager.


### <a name="2-configuration-manager-client-token-request"></a>2. Configuration Manager begäran om klient-token

När klienten har en Azure AD-token begär den en Configuration Manager klient (CCM)-token.

Följande poster loggas i **CCMSetup. log** på den virtuella CMG-datorn:

``` Log
Getting CCM Token from STS server 'CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216'
Getting CCM Token from https://CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216/CCM_STS
```

#### <a name="21-cmg-gets-request"></a>2,1 CMG hämtar begäran

Följande poster loggas i **IIS. log**:

``` Log
RD0003FF74XX2 10.0.0.4 GET /CCM_STS - 443 - HTTP/1.1 python-requests/2.20.0 - - 13.95.234.44 404 0 2 1477 154 15
```

#### <a name="22-cmg-forwards-request-to-cmg-connection-point"></a>2,2 CMG vidarebefordrar begäran till CMG-anslutnings punkten

Följande poster loggas i **CMGService. log**:

``` Log
RequestUri: /CCM_PROXY_SERVERAUTH/XXXXXX037938216/CCM_STS  RequestCount: 769  RequestSize: 1081595 Bytes  ResponseCount: 769     ResponseSize: 36143 Bytes  AverageElapsedTime: 3945 ms
```

#### <a name="23-cmg-connection-point-transforms-cmg-client-request-to-management-point-client-request"></a>2,3 CMG-kopplings punkt transformerar CMG klient förfrågan till hanterings plats klient förfrågan

Följande poster loggas i **SMS_CLOUD_PROXYCONNECTOR. log**:

``` Log
MessageID: 3087bd34-b82c-4950-b972-e82bb0fb8385 RequestURI: https://MP.MYCORP.COM/CCM_STS EndpointName: CCM_STS ResponseHeader: HTTP/1.1 200 OK ~~ ResponseBodySize: 0 ElapsedTime: 2 ms
```

#### <a name="24-management-point-verifies-user-token-in-site-database"></a>hanterings platsen för 2,4 verifierar användartoken i plats databasen

Följande poster loggas i **CCM_STS. log**:

``` Log
Validated AAD token. TokenType: Device TenantId: XXXXe388-XXXX-485c-XXXX-e8e4eb41XXXX UserId: 00000000-0000-0000-0000-000000000000 DeviceId: 0XXXXX80-77XX-4XXa-X63X-67XXXXX64bb7 OnPrem_UserSid:  OnPrem_DeviceSid:

Return token to client, token type: UDA, hierarchyId: XXXX4f9c-XXXX-46a5-XXXX-7612c324XXXX, userId: 00000000-0000-0000-0000-000000000000, deviceId: GUID:XXXXaee9-cXXc-4ccd-XXXX-f1417d81XXX
```


## <a name="content-location-request"></a>Innehålls plats förfrågan

När klienten får ett svar med CCM-token cachelagrar den och använder den för att begära plats information och innehålls plats via CMG. Följande poster loggas i **CCMSetup. log**:

``` Log
Cached encrypted token for 'S-1-5-18'. Will expire at '00/99/2999 00:00:00'
Sending location request to 'CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216' with payload '< Request >
Appending CCM Token to the header.
```


## <a name="client-installation"></a>Klientinstallation

Enheten laddar ned klient innehållet och startar installationen.

### <a name="communication-validation"></a>Kommunikations verifiering

- CMG verifierar klient-token via CMG, CMG Connection Point and HTTP (S) och begäran om hanterings plats databas.
- Klienten verifierar CMG tjänst certifikat eller hanterings certifikat
- PKI för CMG-tjänst certifikat: klienten kräver rot certifikat utfärdare (CA) för CMG-certifikatet i det lokala arkivet
- CMG-tjänst certifikat från tredje part: klienterna validerar automatiskt ett certifikat med dess rot certifikat utfärdare som publicerats på Internet


## <a name="common-issues"></a>Vanliga problem

- Rot certifikat utfärdaren finns inte
- CRL-kontroll aktive rad: publicera CRL på Internet eller Använd alternativet **/NoCRLcheck** på kommando raden
- WPJ-certifikatet hittades inte: klienten har registrerats med Azure AD, men är inte ansluten till Azure AD

Att använda/NoCRLCheck är bara användbart för CCMSetup bootstrap. För att klienterna ska fungera fullt ut bör du publicera listan över återkallade certifikat på Internet. Som en lösning kan du inaktivera CRL-kontrollen på platsens klient kommunikations konfiguration. Annars slutar klienterna att kommunicera med servern efter att säkerhets inställningarna har uppdaterats av plats tjänsten.


## <a name="client-registration"></a>Klient registrering

![Arbets flödes diagram för Azure AD-registrering](media/azure-ad-registration-workflow.png)  

### <a name="1-configuration-manager-client-request-registration"></a>1. Configuration Manager registreringen av klient begär Anden

Följande poster loggas i **ClientIDManagerStartup. log**:

``` Log
[RegTask] - Client is not registered. Sending registration request for GUID:1XXXXXEF-5XX8-4XX3-XEDX-XXXFBFF78XXX ...
Registering client using AAD auth.
```

### <a name="2-configuration-manager-request-azure-ad-token-to-register-client"></a>2. Configuration Manager begära Azure AD-token för att registrera klienten

Följande poster loggas i **ADALOperationProvider. log**:

``` Log
Getting AAD (user) token with: ClientId = f1f9b14e-XXXX-4f17-XXXX-2593f6eee91e, ResourceUrl = https://ConfigMgrService, AccountId = X49FC29A-ECE3-XXX-A3C1-XXXXXXF035A6E
Retrieved AAD token for AAD user '00000000-0000-0000-0000-000000000000'
```

#### <a name="21-configuration-manager-client-is-registered"></a>2,1 Configuration Manager-klienten har registrerats  

Följande poster loggas i **ClientIDManagerStartup. log**:

``` Log
[RegTask] - Client is registered. Server assigned ClientID is GUID:1XXXXXEF-5XX8-4XX3-XEDX-XXXFBFF78XXX. Approval status 3
```

> [!NOTE]  
> Vid klient registrering körs alltid certifikat valideringen. Den här processen sker även om du använder Azure AD-autentiseringsmetoden för att registrera klienten.


### <a name="3-configuration-manager-client-token-request"></a>3. Configuration Manager begäran om klient-token

När platsen registrerar klienten begär klienten en CCM-token. CCM-token krypteras för det lokala system kontot (S-1-5-18) och cachelagras i åtta timmar. Efter åtta timmar upphör token att gälla och klienten begär förnyelse av token.

Följande poster loggas i **ClientIDManagerStartup. log**:

``` Log
Getting CCM Token from STS server 'MP.MYCORP.COM'
Getting CCM Token from https://MP.MYCORP.COM/CCM_STS
...
Cached encrypted token for 'S-1-5-18'. Will expire at 'XX/XX/XX XX:XX:XX'
```

#### <a name="31-cmg-gets-request"></a>3,1 CMG hämtar begäran

Följande poster loggas i **IIS. log**:

``` Log
RD0003FF74XX2 10.0.0.4 GET /CCM_STS - 443 - HTTP/1.1 python-requests/2.20.0 - - 13.95.234.44 404 0 2 1477 154 15
```

#### <a name="32-cmg-forwards-request-to-cmg-connection-point"></a>3,2 CMG vidarebefordrar begäran till CMG-anslutnings punkten

Följande poster loggas i **CMGService. log**:

``` Log
RequestUri: /CCM_PROXY_SERVERAUTH/XXXXXX037938216/CCM_STS  RequestCount: 769  RequestSize: 1081595 Bytes  ResponseCount: 769     ResponseSize: 36143 Bytes  AverageElapsedTime: 3945 ms
```

#### <a name="33-cmg-connection-point-transforms-cmg-client-request-to-management-point-client-request"></a>3,3 CMG-kopplings punkt transformerar CMG klient förfrågan till hanterings plats klient förfrågan

Följande poster loggas i **SMS_CLOUD_PROXYCONNECTOR. log**:

``` Log
MessageID: 3087bd34-b82c-4950-b972-e82bb0fb8385 RequestURI: https://MP.MYCORP.COM/CCM_STS EndpointName: CCM_STS ResponseHeader: HTTP/1.1 200 OK ~~ ResponseBodySize: 0 ElapsedTime: 2 ms
```

#### <a name="34-management-point-verifies-user-token-in-site-database"></a>hanterings platsen för 3,4 verifierar användartoken i plats databasen

Följande poster loggas i **CCM_STS. log**:

``` Log
Validated AAD token. TokenType: Device TenantId: XXXXe388-XXXX-485c-XXXX-e8e4eb41XXXX UserId: 00000000-0000-0000-0000-000000000000 DeviceId: 0XXXXX80-77XX-4XXa-X63X-67XXXXX64bb7 OnPrem_UserSid:  OnPrem_DeviceSid:

Return token to client, token type: UDA, hierarchyId: XXXX4f9c-XXXX-46a5-XXXX-7612c324XXXX, userId: 00000000-0000-0000-0000-000000000000, deviceId: GUID:XXXXaee9-cXXc-4ccd-XXXX-f1417d81XXX
```
