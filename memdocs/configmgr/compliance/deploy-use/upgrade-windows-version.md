---
title: Uppgradera Windows-enheter till en annan version
titleSuffix: Configuration Manager
description: Använd Configuration Manager för att automatiskt uppgradera Windows 10-enheter till en annan Windows-version.
ms.date: 09/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: b0c9db74-841e-46eb-8924-957cde968bf7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 77ef255a820104ef2042a370b5056677fddb9d12
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712234"
---
# <a name="upgrade-windows-devices-to-a-new-edition-with-configuration-manager"></a>Uppgradera Windows-enheter till en ny utgåva med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Med **uppgraderings principen för versionen** kan du automatiskt uppgradera Windows 10-enheter till en annan utgåva.

Följande uppgraderingsvägar stöds:

- Från Windows 10 Pro till Windows 10 Enterprise
- Från Windows 10 Home till Windows 10 Education
- Från Windows 10 Mobile till Windows 10 Mobile Enterprise

Enheterna måste köra Configuration Manager-klient program varan. Enheter som hanteras av [lokal MDM](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) stöds inte.

## <a name="before-you-start"></a>Innan du börjar

Innan du börjar uppgradera enheter till den senaste versionen bör du gå igenom följande krav:  

- För Station ära versioner av Windows 10: en giltig produkt nyckel för den nya versionen av Windows på alla enheter som du riktar principen mot. Den här produkt nyckeln kan vara en MAK (Multiple Activation Key) eller en allmän volym licens nyckel (GVLK). En GVLK kallas även för en klient installations nyckel för nyckel hanterings tjänst (KMS). Mer information finns i [Planera för volym aktivering](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client). En lista över konfigurations nycklar för KMS-klienter finns i [bilaga a](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys) i aktiverings guiden för Windows Server. <!--496871-->  

- För Windows 10 Mobile: en XML-licensserver från Microsoft Volume Licensing Service Center (VLSC). Den här filen innehåller licens information för den nya versionen av Windows på alla enheter som du riktar principen mot.

- Du måste ha säkerhets rollen Configuration Manager **Fullständig administratör** för att kunna hantera den här princip typen.

## <a name="configure-the-policy"></a>Konfigurera principen  

1. I Configuration Manager-konsolen går du till arbets ytan **till gångar och efterlevnad** , **expanderar kompatibilitetsinställningar och**väljer noden **Windows 10-uppgradering** .  

2. Välj **skapa uppgraderings princip för utgåva**i gruppen **skapa** på fliken **Start** i menyfliksområdet.  

3. Välj **Skapa princip**.  

4. Gå till sidan **Allmänt** i **guiden Skapa uppgraderingsprincip för version**och ange följande information:  

    - **Namn** – ange ett namn för uppgraderings principen för versionen  

    - **Beskrivning** (valfritt) – alternativt anger du en beskrivning för principen som hjälper dig att identifiera den i Configuration Manager-konsolen  

    - **SKU för att uppgradera enhet till** – i list rutan väljer du mål utgåvan av Windows 10 Desktop eller Windows 10 Mobile  

    - **Licens information** – Välj något av följande alternativ:  

        - **Produkt nyckel** – ange en giltig produkt nyckel för mål versionen av Windows 10 Desktop Edition  

            > [!NOTE]  
            > När du har skapat en princip som innehåller en produkt nyckel kan du inte redigera produkt nyckeln senare. Configuration Manager skymmer nyckeln av säkerhets skäl. Ändra produkt nyckeln genom att ange hela nyckeln igen.  

        - **Licens fil** – Välj **Bläddra** för att välja en giltig licens fil i XML-format. Configuration Manager använder den här licens filen för att uppgradera Windows 10 Mobile-enheter.  

5. Slutför guiden.  

## <a name="deploy-the-policy"></a>Distribuera principen  

1. I Configuration Manager-konsolen går du till arbets ytan **till gångar och efterlevnad** , **expanderar kompatibilitetsinställningar och**väljer noden **Windows 10-uppgradering** .  

2. Välj den uppgraderings princip för Windows 10-versionen som du vill distribuera. På fliken **Start** i menyfliksområdet väljer du **distribuera**i gruppen **distribution** .  

3. Välj den enhets samling som du vill distribuera principen till.

4. Välj det schema som klienten utvärderar principen för.

5. Slutför guiden.

## <a name="next-steps"></a>Nästa steg

Övervaka den här distributionen från noden **distributioner** på arbets ytan **övervakning** . Om du ser fel som indikerar en misslyckad distribution, till exempel:

- **Ej tillämpad för denna enhet**
- **Konverteringen av datatyp misslyckades**

Dessa fel innebär inte att distributionen misslyckades. Verifiera att uppgraderingen har slutförts på den mål enheten.

När klienten utvärderar mål principen tillämpas uppgraderingen inom två timmar. [Vissa versioner av Windows](https://docs.microsoft.com/windows/deployment/upgrade/windows-10-edition-upgrades) kan kräva en omstart vid detta tillfälle. Se till att du meddelar alla användare som du distribuerar principen till eller schemalägger att principen ska köras utanför användarnas arbets tid.

Om följande fel visas i **DcmWmiProvider. log** på klienten kontrollerar du att du använder rätt nyckel för ditt aktiverings scenario. Mer information finns i avsnittet [innan du börjar](#before-you-start) . Om du använder en nyckel hanterings tjänst (KMS) för aktivering ska du se till att använda en [konfigurations nyckel för KMS-klienten](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys).  <!-- 496871 -->

`Failed to execute CheckApplicabilityMethod with error = 0x80041001 OsEditionUpgradeProvider`

## <a name="see-also"></a>Se även

- [Planera för volym aktivering](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client)

- [Windows 10-utgåveuppgradering](https://docs.microsoft.com/windows/deployment/upgrade/windows-10-edition-upgrades)

- [Uppgradera Windows 10-utgåvor eller växla från S-läge på enheter med Microsoft Intune](https://docs.microsoft.com/intune/edition-upgrade-configure-windows-10)
