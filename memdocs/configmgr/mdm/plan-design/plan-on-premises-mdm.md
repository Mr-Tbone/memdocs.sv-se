---
title: Planera lokal MDM
titleSuffix: Configuration Manager
description: Planera för lokal hantering av mobila enheter för att hantera mobila enheter i Configuration Manager
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 02979fb8-ea7e-4ec6-b7e0-ecbfda73e52d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5690e4fe003939d00dee1185e6f6551813c346e5
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721852"
---
# <a name="plan-for-on-premises-mdm-in-configuration-manager"></a>Planera för lokal MDM i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Det finns flera viktiga områden att granska när du planerar att implementera lokal hantering av mobila enheter (MDM) i Configuration Manager:

- Enheter och OS-versioner som stöds
- Obligatoriska platssystemroller
- Säker kommunikation
- Enhetsregistrering

> [!IMPORTANT]
> Även om platsen eller någon annan mobil enhet inte ansluter till Microsoft Intune, kräver din organisation fortfarande Intune-licenser för att använda den här funktionen. Mer information finns i [Microsoft Intune licensiering](https://docs.microsoft.com/intune/fundamentals/licenses).

Beakta följande krav innan du förbereder Configuration Manager-infrastrukturen för att hantera lokal MDM.

## <a name="supported-devices"></a><a name="bkmk_devices"></a>Enheter som stöds  

Den aktuella grenen av Configuration Manager stöder registrering i lokal hantering av mobila enheter för enheter som kör Windows 10. Dessa enhets typer omfattar främst bärbara datorer, IoT och Surface Hub. Mer information och listan över vissa versioner finns i [operativ system versioner som stöds för klienter och enheter](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS).

## <a name="site-system-roles"></a><a name="bkmk_roles"></a>Plats system roller

Lokal MDM kräver minst en av följande plats system roller:

- **Registreringsproxyplats** som stöd för registreringsbegäranden.

- **Registreringsplats** som stöd för enhetsregistrering.

- **Enhetshanteringsplats** för principleverans. Den här rollen är en variant av hanterings platsen, men möjliggör hantering av mobila enheter.

- **Distributionsplats** för leverans av innehåll.

Beroende på organisationens behov kan du installera dessa roller på en enskild server eller separat på olika servrar.

> [!NOTE]
> Du måste konfigurera varje roll som används för lokal MDM som en HTTPS-slutpunkt för kommunikation med betrodda enheter. Mer information finns i [Nödvändig betrodd kommunikation](#bkmk_trustedComs).

Mer allmän information finns i [Planera för plats system servrar och roller](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).

## <a name="trusted-communications"></a><a name="bkmk_trustedComs"></a>Betrodd kommunikation

Lokal MDM kräver att du aktiverar plats system roller för HTTPS-kommunikation. Du kan använda din organisations certifikat utfärdare (CA) för att upprätta betrodda anslutningar mellan servrar och enheter, beroende på dina behov. Du kan också använda en offentligt tillgänglig certifikat utfärdare som betrodd utfärdare. Båda sätten måste du konfigurera följande certifikat:

- Ett **webb server certifikat** i IIS på de servrar som är värd för de nödvändiga plats system rollerna. Om en server är värd för flera plats system roller behöver du bara ett certifikat för den servern. Om varje roll finns på en separat server behöver varje server ett separat certifikat.

- Det **betrodda rot certifikatet** för den certifikat utfärdare som utfärdar webb server certifikaten. Installera det här rot certifikatet på alla enheter som måste ansluta till plats system rollerna.

Mer information finns i [Konfigurera certifikat för betrodd kommunikation i lokal MDM](../get-started/set-up-certificates-on-premises-mdm.md).

## <a name="device-enrollment"></a><a name="bkmk_enrollment"></a>Enhets registrering

Aktivera enhets registrering för lokal MDM:

- Ge användare behörighet att registrera via klient inställningar

- Konfigurera enheter för betrodd kommunikation med plats system servrar som är värdar för de nödvändiga rollerna

Som ett alternativ till användarinitierad registrering kan du skapa ett Mass registrerings paket. Det här paketet gör att enheten kan registreras utan åtgärder från användaren. Leverera paketet till enheten innan det tillhandahålls för användning eller efter att det går genom dess OOBE-process.

Mer information finns i [Konfigurera enhets registrering för lokal MDM](../get-started/set-up-device-enrollment-on-premises-mdm.md).

## <a name="next-step"></a>Nästa steg

> [!div class="nextstepaction"]
> [Installera platssystemroller](../get-started/install-site-system-roles-for-on-premises-mdm.md)
