---
title: Felsöka vanliga problem för Intune Exchange Connector
titleSuffix: Microsoft Intune
description: Felsök och åtgärda vanliga problem med det lokala Microsoft Intune Exchange-anslutningsprogrammet.
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/06/2020
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
ms.openlocfilehash: b1ed3cd24c05586bd5dc9d9a2443a33ffcdc2a48
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914811"
---
# <a name="resolve-common-problems-with-the-intune-exchange-connector"></a>Lös vanliga problem med Intune Exchange Connector
 
Den här artikeln kan hjälpa Intune-administratören att åtgärda vanliga problem med driften av Intune Exchange Connector.

Innan du börjar söka läser du [Felsöka lokal Intune Exchange-anslutning](troubleshoot-exchange-connector.md) för grundläggande information om anslutningstjänsten. Läs också om vanliga problem vid konfiguration av anslutningsprogram.

## <a name="an-exchange-activesync-device-isnt-discovered-from-exchange"></a>En Exchange ActiveSync-enheten identifieras inte från Exchange

När en Exchange ActiveSync-enhet inte identifieras från Exchange kan du [övervaka Exchange-anslutningens aktivitet](exchange-connector-install.md#on-premises-intune-exchange-connector-high-availability-support) för att se om Exchange-anslutningsprogrammet synkroniserar med Exchange-servern. Om ingen synkronisering har gjorts sedan enheten anslöts samlar du in synkroniseringsloggarna och bifogar dem i en supportbegäran. Om en fullständig synkronisering eller snabb synkronisering har slutförts sedan enheten anslöts söker du efter följande problem:

- Se till att användarna har en Intune-licens. Annars identifierar inte Exchange Connector sina enheter.

- Om användarens primära SMTP-adress skiljer sig från användarhuvudnamnet (UPN) i Azure Active Directory (Azure AD) kan Exchange-anslutningen inte identifiera någon enhet för den användaren. Åtgärda den primära SMTP-adressen för att lösa problemet.

- Om du har både Exchange 2010- och Exchange 2013-postlådeservrar i din miljö rekommenderar vi att du pekar Exchange-anslutningen på en Exchange 2013-klientåtkomstserver (CAS). Om Exchange-anslutningen har konfigurerats för att kommunicera med en Exchange 2010-CAS upptäcker den inga användarenheter på Exchange 2013.

- I Dedikerad Exchange Online-miljöer måste du peka Exchange-anslutningen på en Exchange 2013-CAS (inte en Exchange 2010-CAS) i den dedikerade miljön under den inledande konfigurationen. Anslutningsprogrammet kommunicerar bara med en Exchange 2013-klientåtkomstserver när den kör PowerShell-cmdletar.

## <a name="problems-with-the-notification-email-message"></a>Problem med e-postaviseringen

Om du vill ha stöd för villkorlig åtkomst för lokala postlådor på enheter som inte kör Android Knox kontrollerar du att Intune-registreringen startar från e-postmeddelandet ”Kom igång nu” som Intune Exchange Connector skickar. När du startar registreringen från meddelandet ser du till att enheten tar emot ett unikt ActiveSyncID på alla plattformar (Exchange, Azure AD, Intune).

En användare kanske inte får e-postmeddelandet eftersom:

- Meddelandekontot har konfigurerats felaktigt.
- Det gick inte att identifiera automatiskt för meddelandekontot.
- Begäran om Exchange Web Services (EWS) för att skicka e-postmeddelandet misslyckades.

Läs följande avsnitt för att felsöka problem med e-postavisering.

### <a name="check-the-notification-account-that-retrieves-autodiscover-settings"></a>Kontrollera aviseringskontot som hämtar inställningar för automatisk identifiering

1. Kontrollera att tjänsten för automatisk upptäckt och EWS har konfigurerats på Exchange-klientåtkomstservern. Mer information finns i [Client Access Services](/Exchange/architecture/client-access/client-access) (Klientåtkomsttjänster) och [Tjänsten för automatisk upptäckt i Exchange Server](/Exchange/architecture/client-access/autodiscover?view=exchserver-2019).

2. Kontrollera att ditt aviseringskonto uppfyller följande krav:

   - Kontot har en aktiv postlåda som finns på den lokala Exchange-servern.

   - Kontots UPN matchar SMTP-adressen.

3. För automatisk identifiering krävs en DNS-server som har en DNS-post för **Autodiscover.SMTPdomain.com** (till exempel Autodiscover.contoso.com) som pekar på Exchange-klientens åtkomstserver. Om du vill kontrollera posten anger du FQDN i stället för *Autodiscover.SMTPdomain.com* och följer de här stegen:

   1. Ange *NSLOOKUP*i kommandotolken.

   2. Ange *Autodiscover.SMTPdomain.com*. Utdatan ska likna följande avbildning: ![Nslookup-resultat](./media/troubleshoot-exchange-connector-common-problems/nslookup-results.png
      )

   Du kan också testa tjänsten för automatisk identifiering från Internet på https://testconnectivity.microsoft.com. Eller testa den från en lokal domän med hjälp av Microsoft Connectivity Analyzer-verktyget. Mer information finns i [Microsoft Connectivity Analyzer-verktyget](/previous-versions/office/exchange-remote-connectivity/jj851141(v=exchg.80)).


### <a name="check-autodiscover"></a>Kontrollera automatisk identifiering

Om automatisk identifiering misslyckas kan du prova följande steg:

1. [Konfigurera en giltig DNS-post för automatisk identifiering](/previous-versions/exchange-server/exchange-150/mt473798(v=exchg.150)).

2. Hårdkoda webbadressen i konfigurationsfilen för Intune Exchange Connector:

   1. Fastställ EWS-URL:en. Standard-URL för EWS för Exchange är `https://<mailServerFQDN>/ews/exchange.asmx`, men URL:en kan vara annorlunda. Kontakta Exchange-administratören för att verifiera rätt URL för din miljö.

   2. Redigera filen *OnPremisesExchangeConnectorServiceConfiguration.xml*. Som standard finns filen i *%ProgramData%\Microsoft\Windows Intune Exchange Connector* på den dator som kör Exchange-anslutningsprogrammet. Öppna filen i en textredigerare och ändra sedan följande rad så att den återspeglar EWS-URL:en för din miljö: `<ExchangeWebServiceURL>https://<YourExchangeHOST>/EWS/Exchange.asmx</ExchangeWebServiceURL>`

3. Spara filen och starta om datorn eller Microsoft Intune Exchange Connector-tjänsten.

>[!NOTE]
> I den här konfigurationen slutar Intune Exchange Connector att använda automatisk identifiering och ansluter istället direkt till EWS-URL:en.

## <a name="next-steps"></a>Nästa steg

Om du vill ha hjälp med specifika problem kan du prova med [Åtgärda vanliga fel för Intune Exchange Connector](troubleshoot-exchange-connector-common-errors.md).

Gör så här för att få support eller för hjälp från Intune-communityn:

- Se [Få support](../fundamentals/get-support.md) om att använda Intune-konsolen till att felsöka problemet, eller för att öppna ett supportärende hos Microsoft.
- Publicera ditt problem i [Microsoft Intunes forum](https://social.technet.microsoft.com/Forums/home?forum=microsoftintuneprod).