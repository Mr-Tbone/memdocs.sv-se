---
title: Installera Exchange Connector
titleSuffix: Configuration Manager
description: Installera och konfigurera Exchange-anslutaren för Configuration Manager för att hantera mobila enheter via ActiveSync.
ms.date: 12/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: e179e30a-a1fc-461e-8087-ff3a55803450
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e0db550369ca2d81f42a25e68960b5f8f27be168
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700488"
---
# <a name="install-and-configure-the-exchange-connector"></a>Installera och konfigurera Exchange Connector

*Gäller för: Configuration Manager (aktuell gren)*

Använd den här proceduren för att installera och konfigurera en Exchange Server-anslutning för att hantera mobila enheter. Configuration Manager har bara stöd för en anslutning i en Exchange-organisation.

Kontrol lera att du har de behörigheter och versioner som krävs innan du installerar Exchange Server-anslutningen för Configuration Manager. Mer information finns i [enhets hantering med Exchange och Configuration Manager](manage-mobile-devices-with-exchange-activesync.md#prerequisites).

## <a name="exchange-connection-account"></a>Konto för Exchange-anslutning

Bestäm vilket konto som ska ansluta till Exchange-klientåtkomstservern för att hantera de mobila enheterna. Kontot kan vara platsserverns datorkonto eller ett Windows-användarkonto.

Konfigurera sedan det här kontot i en Exchange-roll grupp för att köra följande Exchange Server-cmdletar:

- **Clear-ActiveSyncDevice**  

- **Get-ActiveSyncDevice**  

- **Get-ActiveSyncDeviceAccessRule**  

- **Get-ActiveSyncDeviceStatistics**  

- **Get-ActiveSyncMailboxPolicy**  

- **Get-ActiveSyncOrganizationSettings**  

- **Get-ExchangeServer**  

- **Hämta post låda**

- **Get-Recipient**  

- **Set-ADServerSettings**  

- **Set-ActiveSyncDeviceAccessRule**  

- **Set-ActiveSyncMailboxPolicy**  

- **Set-CASMailbox**  

- **New-ActiveSyncDeviceAccessRule**  

- **New-ActiveSyncMailboxPolicy**  

- **Remove-ActiveSyncDevice**  

- **Get-CasMailbox**  

- **Get-User**  

- **Set-ActiveSyncOrganizationSettings**  

Följande Exchange Server-hanterings roller innehåller dessa cmdlet: ar:

- Hantering av mottagare
- Visa endast organisations hantering
- Serverhantering

Mer information finns i [förstå roll grupper för hantering](/exchange/understanding-management-role-groups-exchange-2013-help) i Exchange Server 2013-dokumentationen.

> [!TIP]  
> Om du försöker installera eller använda Exchange Server-anslutningen utan nödvändiga cmdletar visas följande fel i filen EasDisc. log på plats serverdatorn: `Invoking cmdlet <cmdlet> failed` .

## <a name="install-the-connector"></a>Installera anslutningen

1. I Configuration Manager-konsolen går du till arbets ytan **Administration** , expanderar **konfiguration av hierarki**och väljer sedan **Exchange Server-kopplingar**.

1. Välj **Lägg till Exchange Server**i gruppen **skapa** på fliken **Start** i menyfliksområdet.

1. Välj en av Exchange Server-miljöerna på sidan **Allmänt** i guiden Lägg till Exchange Server:

    - **Lokal Exchange Server**: Ange en enskild server eller en klient åtkomst Server mat ris för varje Active Directory plats.

        Om servern eller matrisen är offline försöker Configuration Manager identifiera en klient åtkomst server att använda. Om detta Miss lyckas går Configuration Manager tillbaka till att använda en post låda-Server för att upprätta en anslutning till en klient åtkomst Server. När den försöker ansluta igen loggar den följande varningar i filen EasDisc. log på plats serverdatorn: `Failed to open runspace for site <site_name>` .

    - **Värdbaserad Exchange Server**: Ange Server adressen till Exchange Online-miljön.

    Välj den primära platsen för att köra Exchange Server-anslutningen.

1. På sidan **konto** anger du det konto som ska anslutas till Exchange-servern. Mer information finns i [Exchange Connection-konto](#exchange-connection-account).

1. På sidan **identifiering** konfigurerar du synkroniseringsschemat och regler för att söka efter enheter.

1. På sidan **Inställningar** konfigurerar du inställningarna för mobila enheter i följande grupper:

    - **Allmänt**
    - **Lösenord**
    - **E-posthantering**
    - **Säkerhet**
    - **Program**

    Mer information finns i [Exchange Connector-inställningar](manage-mobile-devices-with-exchange-activesync.md#policies).

    Om du även registrerar mobila enheter med Configuration Manager [lokal MDM](../understand/manage-mobile-devices-with-on-premises-infrastructure.md), aktiverar du alternativet för att **tillåta extern hantering av mobila enheter**. Med den här inställningen kan de mobila enheterna fortsätta att ta emot e-post från Exchange efter att Configuration Manager registrerat dem.

1. Slutför guiden.

## <a name="verify-and-monitor"></a>Verifiera och övervaka

Verifiera installationen av Exchange Server-anslutningen med status meddelanden och loggfiler:

- Bekräfta att Platskomponenthanteraren har installerat Exchange Server-anslutningen. Leta efter meddelande status ID **1015** från **SMS_EXCHANGE_CONNECTOR** -komponenten.

    Det går inte att installera om den angivna klient åtkomst servern är offline. Om Configuration Manager inte kan installera anslutningen kan Configuration Manager försöka installera igen var 60: e minut. Det fortsätter att försöka tills installationen lyckas eller också tar du bort Exchange Server-anslutningen.

- På plats serverdatorn granskar du **SiteComp. log** efter följande post: `Component SMS_EXCHANGE_CONNECTOR flagged for installation` . Därefter loggas den slutförda installationen med följande text: `STATMSG: ID=1015` .

När du har slutfört installationen övervakar du de mobila enheter som hittas och hanteras av anslutnings tjänsten. Visa samlingarna med mobila enheter och Använd rapporterna för mobila enheter.

> [!NOTE]  
> Configuration Manager skapar namn för de mobila enheter som hittas. Det använder formatet *användar namn*_*enhets typ*. Till exempel **jdoe_WindowsPhone**. Om en användare har mer än en mobil enhet som har samma enhets typ, visar Configuration Manager samma namn för dessa mobila enheter i-konsolen och i rapporter.  

## <a name="see-also"></a>Se även

- [Portar som används av konfigurations klienter och plats system](../../core/plan-design/hierarchy/ports.md#BKMK_PortsExchangeConnectorHosted)
- [Stöd för proxyserver](../../core/plan-design/network/proxy-server-support.md#site-system-roles-that-use-a-proxy)
- [Säkerhets rekommendationer för mobila enheter](../../core/clients/deploy/plan/security-and-privacy-for-clients.md#bkmk_mobile)
- [Sekretess information för mobila enheter som hanteras med Exchange Server-anslutningen](../../core/clients/deploy/plan/security-and-privacy-for-clients.md#BKMK_Privacy_ExchangeConnector)