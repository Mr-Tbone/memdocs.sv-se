---
title: Enhetshantering med Exchange
titleSuffix: Configuration Manager
description: Hantera mobila enheter med Exchange Server-anslutningen i Configuration Manager.
ms.date: 12/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: aba688d9-fd5b-4c42-8cb4-f7e1b161ef50
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 08d92d5c09331d675dc679a374e1bbf81633748e
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721929"
---
# <a name="device-management-with-exchange-and-configuration-manager"></a>Enhets hantering med Exchange och Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Om du har mobila enheter som du ansluter till Exchange Server via ActiveSync-protokollet kan du använda Exchange Server-anslutningen i Configuration Manager för att hantera dessa enheter. Anslutningen fungerar med både lokal Exchange Server eller Exchange Online. Använd Configuration Manager-konsolen för att konfigurera funktioner för hantering av mobila enheter i Exchange. Till exempel fjärrenhets rensning och inställnings kontroll för flera Exchange-servrar.

![Logiskt diagram för Exchange Server-anslutning med Configuration Manager](media/configmgr-with-exchange.png)  

När du hanterar mobila enheter med den här anslutnings tjänsten installerar den inte Configuration Manager klienten eller registrerar enheterna via MDM. Hanterings funktionerna i Exchange Server är begränsade i jämförelse med de här andra alternativen. Du kan t. ex. inte installera program vara eller använda konfigurations objekt för att konfigurera dessa enheter. Mer information finns i [Välj en lösning för enhets hantering för Configuration Manager](../../core/plan-design/choose-a-device-management-solution.md).  

## <a name="policies"></a>Principer

När du använder-anslutningen konfigurerar Configuration Manager inställningar på de mobila enheterna. Enheterna använder inte standard principerna för Exchange ActiveSync-postlådan. Definiera de inställningar som du vill använda i följande grupper:

- **Allmänt**
- **Lösenord**
- **E-posthantering**
- **Säkerhet**
- **Program**

I gruppen **lösen ord** kan du till exempel konfigurera följande inställningar:

- Huruvida mobila enheter kräver ett lösen ord
- Minsta längd på lösen ord
- Lösenordskomplexitet
- Om lösen ords återställning tillåts

När du konfigurerar minst en inställning i gruppen hanterar Configuration Manager alla inställningar i gruppen för mobila enheter. Om du inte konfigurerar någon inställning i en grupp fortsätter Exchange att hantera de här inställningarna för de mobila enheterna. Alla Exchange ActiveSync-postlådor som du konfigurerar på Exchange-servern och tilldelar användare används fortfarande.

## <a name="access-rules-and-remote-actions"></a>Åtkomst regler och fjärråtgärder

Du kan också konfigurera Exchange Server-anslutningen för att hantera åtkomst regler för Exchange. De här åtkomst reglerna är Tillåt-, block-eller karantän mobila enheter. Du kan fjärrrensa mobila enheter med hjälp av Configuration Manager-konsolen och användare kan fjärrrensa sina mobila enheter med hjälp av program katalogen.

En användares mobila enhet visas automatiskt i program katalogen när du hanterar den och Exchange-servern är lokal. Konfigurera mappning mellan användare och enhet manuellt för den mobila enheten som ska visas i program katalogen när du använder Exchange Online. Mer information finns i [Länka användare och enheter med mappning mellan användare och enhet](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

> [!TIP]  
> När en mobil enhet överförs till en annan användare måste du ta bort den mobila enheten från Configuration Manager-konsolen innan den nya ägaren konfigurerar sitt Exchange-konto på enheten.

## <a name="prerequisites"></a>Krav

> [!IMPORTANT]  
> Innan du installerar den här anslutningen ska du kontrol lera att Configuration Manager stöder din version av Exchange. Mer information finns i [konfigurationer som stöds-Exchange Server-anslutning](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_ExSrvConOS).  

### <a name="permissions-to-configure-the-connector"></a>Behörigheter för att konfigurera anslutningen

Du behöver följande säkerhets behörigheter för att konfigurera Exchange Server-anslutningen i Configuration Manager:

- Så här lägger du till, ändrar eller tar bort Exchange Server-anslutningen: behörigheten **Ändra** för objektet **Plats** .  

- Konfigurera inställningar för mobila enheter: behörigheten **ModifyConnectorPolicy** för objektet **Plats** .  

Den inbyggda rollen **Fullständig administratör** inkluderar till exempel de nödvändiga behörigheterna.  

### <a name="permissions-to-manage-mobile-devices"></a>Behörigheter för att hantera mobila enheter

Du behöver följande säkerhets behörigheter för att hantera mobila enheter:  

- Rensa en mobil enhet: **Ta bort resurs** för objektet **Samling** .  

- Annullera ett rensningskommando: **Ändra resurs** för objektet **Samling** .  

- Tillåta och blockera mobila enheter: **Ändra resurs** för objektet **Samling** .  

Den inbyggda rollen **drifts administratör** innehåller till exempel de behörigheter som krävs.

Mer information finns i [Konfigurera rollbaserad administration](../../core/servers/deploy/configure/configure-role-based-administration.md).

## <a name="next-steps"></a>Nästa steg

> [!div class="nextstepaction"]
> [Installera och konfigurera Exchange Connector](install-configure-exchange-connector.md)
