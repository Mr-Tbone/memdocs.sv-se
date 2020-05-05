---
title: Hur användare registrerar enheter
titleSuffix: Configuration Manager
description: Förstå hur användare registrerar enheter med lokal hantering av mobila enheter (MDM) i Configuration Manager.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 59004b34-b64f-4d77-898c-07bf3dc75430
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f80b77d6a25d7af701ded249118e95201bcb9cc1
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722335"
---
# <a name="how-users-enroll-devices-with-on-premises-mdm-in-configuration-manager"></a>Hur användare registrerar enheter med lokal MDM i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Med Configuration Manager lokal hantering av mobila enheter (MDM) kan användare registrera sina enheter. Det finns två krav:

- Med klient inställningarna ger du användaren behörighet att registrera.

- Du installerar det betrodda rot certifikatet som krävs på enheten.

Mer information om hur du konfigurerar registrering finns i [Konfigurera enhets registrering för lokal MDM](../get-started/set-up-device-enrollment-on-premises-mdm.md).

## <a name="enroll-windows-10"></a><a name="bkmk_enrollDesk"></a>Registrera Windows 10

1. Besök **Inställningar**på en Windows 10-dator.

1. Välj **konton**och välj sedan **åtkomst till arbete eller skola**.

1. Välj **Anslut**, ange din User Principal Name (UPN) och välj **Fortsätt**. UPN kan vara detsamma som din e-postadress, till exempel jdoe@contoso.com.

1. Ange det fullständigt kvalificerade domän namnet (FQDN) för proxyn för registrerings platsen och välj **Fortsätt**.

1. Ange ditt lösen ord och välj **Logga**in.

1. Windows behöver inte komma ihåg inloggnings informationen för den här åtgärden, så välj **hoppa över**.

Efter en kort tid registrerar enheten med Configuration Manager.

## <a name="enroll-windows-10-mobile"></a><a name="bkmk_enrollMob"></a>Registrera Windows 10 Mobile

1. Besök **Inställningar**på en enhet med Windows 10 Mobile.

1. Välj **konton**och välj sedan **åtkomst till arbets**plats.

1. Välj **Anslut**.

1. Ange ditt UPN och FQDN för proxyn för registrerings platsen. Välj **Anslut**.

1. På nästa skärm anger du ditt UPN och lösen ord och väljer sedan **Logga**in.

Efter en kort tid registrerar enheten med Configuration Manager. Välj **Klar**.

## <a name="verify-enrollment"></a><a name="bkmk_verify"></a>Verifiera registrering

Använd Configuration Manager-konsolen för att verifiera att enheterna har registrerats. Gå till arbets ytan **till gångar och efterlevnad** i Configuration Manager-konsolen och välj **enheter**. Bläddra eller Sök efter den registrerade enheten i listan med enheter.
