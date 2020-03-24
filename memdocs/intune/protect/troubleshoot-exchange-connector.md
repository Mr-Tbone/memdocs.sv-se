---
title: Felsöka Exchange Connector
titleSuffix: Microsoft Intune
description: Felsöka problem med lokal Intune Exchange-anslutning.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/02/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: a7e3c742-295b-40bb-9afa-17f243062500
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: af44b09f5e539306a24ae0e0294b3ad674f7cb74
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79338558"
---
# <a name="troubleshoot-the-intune-exchange-connector"></a>Felsöka Intune Exchange Connector

I den här artikeln beskrivs hur du felsöker problem med Intune Exchange Connector.

## <a name="before-you-start"></a>Innan du börjar

Innan du börjar felsöka ett Exchange Connector-problem i Intune samlar du in viss grundläggande information så att du har en bra grund att utgå från. Med den här metoden blir det lättare att förstå problemets beskaffenhet och lösa det snabbare.

- Kontrollera att processen uppfyller installationskraven. Mer information finns i [Konfigurera lokala Intune Exchange Connector](exchange-connector-install.md).
- Kontrollera att ditt konto har både Exchange- och Intune-administratörsbehörighet.
- Anteckna den fullständiga och exakta felmeddelandetexten, informationen och var meddelandet visas.
- Ta reda på när problemet startade: 
  - Konfigurerar du anslutningsprogrammet för första gången? 
  - Fungerade anslutningsprogrammet korrekt och kunde sedan inte köras?
  - Om det fungerade, vilka ändringar gjordes i Intune-miljön, Exchange-miljön eller på datorn som kör anslutningsprogrammet?
- Vad är MDM-utfärdare?
- Vilken version av Exchange använder du?

### <a name="use-powershell-to-get-more-data-on-exchange-connector-issues"></a>Använda PowerShell för att få mer information om problem med Exchange Connector

- Använd `Get-ActiveSyncDeviceStatistics -mailbox mbx` om du vill hämta en lista med alla mobila enheter för en postlåda
- Använd `Get-Mailbox -Identity user | select emailaddresses | fl` om du vill hämta en lista med alla SMTP-adresser för en postlåda
- Om du vill hämta detaljerad information om en enhets åtkomststatus använder du `Get-CASMailbox <upn> | fl`

## <a name="review-the-connector-configuration"></a>Granska anslutningsprogrammets konfiguration

Granska [de lokala kraven för Exchange-anslutningsprogram](exchange-connector-install.md#intune-exchange-connector-requirements) för att se till att din miljö och anslutningsprogrammet är rätt konfigurerade. 

### <a name="general-considerations-for-the-connector"></a>Allmänna överväganden för anslutningsprogrammet

- Kontrollera att brandvägg och proxyservrar tillåter kommunikation mellan servern som är värd för Intune Exchange Connector och Intune-tjänsten.

- Datorn som är värd för Intune Exchange Connector och Exchange-klientens åtkomstserve måste vara domänansluten och i samma LAN. Kontrollera att de nödvändiga behörigheterna har lagts till för kontot som används av Intune Exchange Connector.

- Aviseringskontot används till att hämta inställningar för *automatisk upptäckt*. Mer information om automatisk upptäckt i Exchange finns i [Tjänsten för automatisk upptäckt i Exchange Server](https://docs.microsoft.com/exchange/architecture/client-access/autodiscover?view=exchserver-2016).

- Intune Exchange Connector skickar en begäran till EWS-URL:en med hjälp av autentiseringsuppgifterna för aviseringskontot, för att skicka aviseringar via e-post tillsammans med länken *Kom igång* (för att registrera i Intune). Användning av *Kom igång*-länken för registrering är ett krav för Android-enheter som inte har Knox. Annars kommer dessa enheter att blockeras av den villkorsstyrda åtkomsten.

### <a name="common-issues-for-connector-configurations"></a>Vanliga problem vid konfiguration av anslutningsprogram

- **Kontobehörigheter**: I dialogrutan för Microsoft Intune Exchange Connector ser du till att du har angett ett användarkonto som har nödvändiga behörigheter för att köra [Windows PowerShell Exchange-cmdlets](exchange-connector-install.md#exchange-cmdlet-requirements).
- **E-postadresser för meddelanden**: Aktivera meddelanden och ange ett meddelandekonto.
- **Synkronisering av klientåtkomstserver**: När du konfigurerar Exchange Connector anger du en klientåtkomstserver med kortast möjliga svarstid för den server som är värd för Exchange-anslutningsprogrammet. Svarstiden för kommunikationen mellan klientåtkomstservern och Exchange-anslutningen kan orsaka fördröjningar i enhetsidentifieringen, särskilt om Dedikerad Exchange Online används.
- **Synkroniseringsschema**: Åtkomst för en användare med en nyligen registrerad enhet kan fördröjas tills Exchange-anslutningen synkroniserar med Exchange-CAS. En fullständig synkronisering görs en gång per dag, och en deltasynkronisering (snabbsynkronisering) görs flera gånger per dag. Du kan [manuellt framtvinga en snabbsynkronisering eller en fullständig synkronisering](exchange-connector-install.md#manually-force-a-quick-sync-or-full-sync) för att minimera fördröjningar.

## <a name="next-steps"></a>Nästa steg
Följande artiklar kan hjälpa till att lösa vanliga problem och specifika fel:

- [Lös vanliga problem för Intune Exchange Connector](troubleshoot-exchange-connector-common-problems.md).
- [Lös vanliga fel för Intune Exchange Connector](troubleshoot-exchange-connector-common-errors.md).

Sök hjälp från supporten eller Intune-communityn:

- Se [Få support](../fundamentals/get-support.md) om att använda Intune-konsolen till att felsöka problemet, eller för att öppna ett supportärende hos Microsoft. 
- Publicera ditt problem i [Microsoft Intunes forum](https://social.technet.microsoft.com/Forums/en-US/home?forum=microsoftintuneprod).  