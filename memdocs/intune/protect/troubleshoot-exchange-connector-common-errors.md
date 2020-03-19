---
title: Felsök vanliga fel för Intune Exchange Connector
titleSuffix: Microsoft Intune
description: Felsök och åtgärda vanliga fel för den lokala Microsoft Intune Exchange Connector
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/02/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: cb35fdc400c89c64b689f4695a48d201e50fc617
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79350661"
---
# <a name="resolve-common-errors-for-the-intune-exchange-connector"></a>Åtgärda vanliga fel för Intune Exchange Connector

Den här artikeln kan hjälpa Intune-tjänstadministratören att åtgärda vissa fel och meddelanden om driften av Intune Exchange Connector.  

## <a name="configuration-failed-and-returned-error-code-0x0000001"></a>Konfigurationen misslyckades och returnerade felkoden 0x0000001

**Problem**:  
När du försöker konfigurera Microsoft Intune Exchange Connector får du följande felmeddelande:

```
   The Microsoft Intune Exchange Connector cannot connect to the Microsoft Exchange server.  
   The following Microsoft Exchange Server address could not be reached <Exchange server Name FQDN>  
   Verify that the FQDN of the exchange server address and credentials that you entered is correct and the server is running. The Microsoft Intune Exchange Connector does not support Exchange server arrays.  
   Error code: 0x0000001  
```

Det här problemet kan uppstå om Internetproxyinställningarna för har konfigurerats fel.

**Lösning**:  
Konfigurera proxyinställningar:
1. Kontakta administratören för det lokala nätverket för att se till att proxyinställningarna är korrekt konfigurerade. 
2. Använd kommandot **Netsh winhttp** för att konfigurera proxyservern och lägga till den undantagslista som krävs. Exempel:  

   ```
   Netsh winhttp set proxy proxy-server="http=proxy.corp.domain.com" bypass-list"34*.*;134.132.*.*;10.*.*;localhost;*.corp.domain.com;*.staging.domain.com"
   ```

## <a name="configuration-failed-and-returned-error-code-0x000000b"></a>Konfigurationen misslyckades och returnerade felkoden 0x000000b   

**Problem**:  
När du försöker konfigurera Microsoft Intune Exchange Connector får du följande felmeddelande:  

```
   The Microsoft Intune Exchange Connector experienced an error:  
   CertEnroll::CX509PrivateKey::Create: The system cannot find the file specified. 0x80070002 (WIN32: 2  
   ERROR_FILE_NOT_FOUND  
   Error code: 0x000000b  
```
Det här problemet kan uppstå om kontot som du använde för att logga in på Intune inte är ett globalt administratörskonto för Intune.

**Lösning**:  
Logga in på Intune med ett konto som är en global administratör eller lägg till ditt konto i den globala administratörsgruppen. Mer information finns i [Rollbaserad administrationskontroll (RBAC) med Microsoft Intune](../fundamentals/role-based-access-control.md).

## <a name="configuration-failed-and-returned-error-code-0x0000006"></a>Konfigurationen misslyckades och returnerade felkoden 0x0000006

**Problem**:  
När du försöker konfigurera Microsoft Intune Exchange Connector får du följande felmeddelande:  

```  
   The Microsoft Intune Exchange Connector cannot connect to Microsoft Intune  
   Verify that you are connected to the Internet, check the Microsoft Intune Service Status, and try to connect again.  
   Error code: 0x00000006  
```  
Det här felet kan uppstå om en proxyserver används för anslutning till Internet och den blockerar trafiken till Intune-tjänsten. Kontrollera om en proxy används. Gå till **Kontrollpanel** > **Internetalternativ**, välj fliken **Anslutning** och klicka sedan på **LAN-inställningar**.

**Lösning**:  

- **Alternativ 1** – Ta bort proxyinställningarna så att datorn kan ansluta till Internet utan att gå via proxyn.  

- **Alternativ 2** – Konfigurera proxyservern så att den tillåter kommunikation med Intune-tjänsten, enligt beskrivningen i [Krav för Intune Exchange Connector](exchange-connector-install.md#intune-exchange-connector-requirements).



## <a name="event-7000-or-7041-microsoft-intune-exchange-connector-service-wont-start"></a>Händelse 7000 eller 7041: Tjänsten Microsoft Intune Exchange Connector startar inte

**Problem**:  
En iOS-enhet kan inte registreras i Intune och genererar något av följande felmeddelanden:  

```  
   Log Name:      System
   Source:            Service Control Manager
   Date:               <time>
   Task Category: None
   Level:               Error
   Keywords:        Classic
   User:                N/A
   Computer:      <computer>
   Description:
   The Microsoft Intune Exchange Connector Service service failed to start because of the following error:  
   The service did not start because of a logon failure.
```  

```  
   Log Name:      System
   Source:            Service Control Manager
   Date:               <time>
   Event ID:          7041
   Task Category: None
   Level:               Error   
   Keywords:        Classic
   User:                N/A
   Computer:       <computer>
   Description:
   The WIEC service was unable to log on as .\WIEC_USER with the currently configured password because of the following error:
   Logon failure: the user has not been granted the requested logon type at this computer.
   Service: WIEC
   Domain and account: .\WIEC_USER
   This service account does not have the required user right "Log on as a service."  
```
Det här problemet kan uppstå om kontot **WIEC_User** inte har användarbehörigheten **Logga in som en tjänst** i den lokala principen.

**Lösning**:  
På den dator som kör Intune Exchange Connector tilldelar du användarbehörigheten **Logga in som en tjänst** till tjänstkontot **WIEC_User**. Om datorn är en nod i ett kluster tilldelar du användarrättigheten *Logga in som en tjänst* till klustertjänstkontot på alla noder i klustret.  

Följ de här anvisningarna om du vill tilldela användarbehörigheten **Logga in som en tjänst** till tjänstkontot **WIEC_User** på datorn:

1. Logga in på datorn som administratör eller med ett konto som är medlem i gruppen Administratörer.
2. Kör **secpol.msc** för att öppna den lokala säkerhetsprincipen.
3. Gå till **Säkerhetsinställningar** > **Lokala principer** och välj **Tilldelning av användarrättigheter**.
4. I den högra rutan dubbelklickar du på **Logga in som en tjänst**.
5. Välj **Lägg till användare eller grupp**, lägg till **WIEC_USER** till principen och välj sedan **OK** två gånger.

Om användarrättigheten **Logga in som en tjänst** har tilldelat till **WIEC_User** men senare har tagits bort kontaktar du domänadministratören för att ta reda på om den skrivs över av en grupprincipinställning.  

## <a name="next-steps"></a>Nästa steg  

Följande artikel kan hjälpa dig att åtgärda specifika fel:
- [Åtgärda vanliga problem för Intune Exchange Connector](troubleshoot-exchange-connector-common-problems.md).git 

Sök hjälp från supporten eller Intune-communityn.
- Se [Få support](../fundamentals/get-support.md) om att använda Intune-konsolen till att felsöka problemet, eller för att öppna ett supportärende hos Microsoft. 
- Publicera ditt problem i [Microsoft Intunes forum](https://social.technet.microsoft.com/Forums/en-US/home?forum=microsoftintuneprod).  
