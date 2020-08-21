---
title: Installera platssystemroller
titleSuffix: Configuration Manager
description: Lägg till plats system roller till en befintlig eller ny plats system server på platsen.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 61f5c774-7667-44ae-b8e4-a4951318b183
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 30b57de75e637aa083070832783647b8ad35b4a7
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700539"
---
# <a name="install-site-system-roles-for-configuration-manager"></a>Installera plats system roller för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Det finns två metoder i Configuration Manager-konsolen för att installera plats system roller:

- **Lägg till plats system roller**: Lägg till plats system roller till en befintlig plats system server på platsen.

- **Skapa plats system Server**: Ange en ny server som plats system Server och installera sedan en eller flera roller. Den här metoden är samma som för att **lägga till plats system roller**, förutom den första sidan. Du anger först namnet på servern och den plats där du vill installera den.

> [!TIP]
> När du installerar en roll på en fjärrdator Configuration Manager lägger till dator kontot för fjärrdatorn i en lokal grupp på plats servern.
>
> När du installerar platsen på en domänkontrollant är gruppen på plats servern en domän grupp istället för en lokal grupp. I det här fallet fungerar inte fjärrplatsens system roll omedelbart. Plats system servern måste startas om eller så uppdaterar du Kerberos-biljetten för fjärrserverns dator konto. Mer information finns i [konton som används](../../../plan-design/hierarchy/accounts.md).

Innan den installerar plats system rollen kontrollerar Configuration Manager mål datorn för att kontrol lera att den uppfyller kraven för de valda rollerna.

När Configuration Manager installerar en plats system roll installeras som standard filer på den första tillgängliga NTFS-formaterade disk enheten som har mest ledigt disk utrymme. För att förhindra Configuration Manager från att installeras på vissa enheter, innan du installerar plats system servern, skapar du en tom fil med namnet **No_sms_on_drive. SMS** i roten på enheten.

Configuration Manager använder **kontot för installation av plats system** för att installera roller. Du anger det här kontot när du installerar rollen. Som standard är det här kontot det lokala system kontot för plats serverdatorn. Du kan ange ett domän användar konto som konto för installation av plats system. Mer information finns i [konton-plats system installations konto](../../../plan-design/hierarchy/accounts.md#site-system-installation-account).

## <a name="install-roles-on-an-existing-site-system-server"></a><a name="bkmk_addrole"></a> Installera roller på en befintlig plats system Server

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen. Expandera **plats konfiguration**och välj noden **servrar och plats system roller** . Välj den befintliga plats system server där du vill installera nya plats system roller.

1. I menyfliksområdet på fliken **Start** går du till gruppen **Server** och väljer **Lägg till plats system roller**.

1. På sidan **Allmänt** granskar du inställningarna.

    > [!TIP]
    >  För att få åtkomst till plats system rollen från Internet, se till att du anger ett fullständigt kvalificerat domän namn (FQDN) för Internet.

1. Om roller på den här servern kräver en Internet-proxy på sidan **proxy** anger du inställningarna för en proxyserver. Mer information finns i [stöd för proxy server](../../../plan-design/network/proxy-server-support.md).

1. På sidan **urval för system roll** väljer du de plats system roller som du vill lägga till.

1. Slutför guiden. Ytterligare sidor kan visas för vissa roller. Mer information finns i [konfigurations alternativ för plats system roller](configuration-options-for-site-system-roles.md).

> [!TIP]
> Windows PowerShell-cmdleten **New-CMSiteSystemServer**utför samma funktion som den här proceduren. Mer information finns i [New-CMSiteSystemServer](/powershell/module/configurationmanager/new-cmsitesystemserver?view=sccm-ps).

## <a name="install-roles-on-a-new-site-system-server"></a><a name="bkmk_createnew"></a> Installera roller på en ny plats system Server

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen. Expandera **plats konfiguration**och välj noden **servrar och plats system roller** .

1. Välj **skapa plats system Server**i gruppen **skapa** på fliken **Start** i menyfliksområdet.

1. På sidan **Allmänt** anger du allmänna inställningar för plats systemet.

    > [!TIP]
    > För att komma åt den nya plats system rollen från Internet måste du kontrol lera att du anger ett fullständigt domän namn för Internet.

1. Om roller på den här servern kräver en Internet-proxy på sidan **proxy** anger du inställningarna för en proxyserver. Mer information finns i [stöd för proxy server](../../../plan-design/network/proxy-server-support.md).

1. På sidan **urval för system roll** väljer du de plats system roller som du vill lägga till.

1. Slutför guiden. Ytterligare sidor kan visas för vissa roller. Mer information finns i [konfigurations alternativ för plats system roller](configuration-options-for-site-system-roles.md).

> [!TIP]
> Windows PowerShell-cmdleten **New-CMSiteSystemServer**utför samma funktion som den här proceduren. Mer information finns i [New-CMSiteSystemServer](/powershell/module/configurationmanager/new-cmsitesystemserver?view=sccm-ps).

## <a name="next-steps"></a>Nästa steg

- [Konfigurationsalternativ för platssystemroller](configuration-options-for-site-system-roles.md)

- [Ta bort roll](../install/uninstall-sites-and-hierarchies.md#bkmk_role)