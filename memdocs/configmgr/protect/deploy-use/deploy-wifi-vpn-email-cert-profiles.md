---
title: Distribuera resursåtkomstprofiler
titleSuffix: Configuration Manager
description: Lär dig hur du distribuerar Wi-Fi-, VPN-och certifikat profiler i Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3753608d-b539-44dc-8e3f-b631319e7687
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0272c50429973cc3e15c295303b91593075ebe01
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724519"
---
# <a name="deploy-resource-access-profiles-in-configuration-manager"></a>Distribuera resurs åtkomst profiler i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

När du har skapat någon av följande resurs åtkomst profiler distribuerar du den till en eller flera samlingar:

- [Wi-Fi](create-wifi-profiles.md)
- [VPN](create-vpn-profiles.md)
- [Certifikatmallens](create-certificate-profiles.md)

När du distribuerar de här profilerna anger du mål samlingen och anger hur ofta klienten utvärderar profilen för efterlevnad.  

## <a name="deploy-a-profile"></a>Distribuera en profil

1. Gå till arbets ytan **till gångar och efterlevnad** i Configuration Manager-konsolen. Expandera **kompatibilitetsinställningar, expandera** **åtkomst till företags resurser**och välj sedan lämplig profil-nod. Till exempel **Wi-Fi-profiler**.

1. I listan över profiler väljer du den profil som du vill distribuera. På fliken **Start** i menyfliksområdet väljer du **distribuera**i gruppen **distribution** .  

1. I fönstret distribuera profil anger du följande information:  

    - **Samling**: Välj den samling där du vill distribuera profilen.

    - **Generera en varning**: aktivera det här alternativet om du vill konfigurera en avisering. Platsen genererar den här aviseringen om profilens efterlevnad är mindre än den angivna procent andelen vid angivet datum och tid. Du kan också välja om du vill att en avisering ska skickas till System Center Operations Manager.

    - **Slumpmässig fördröjning (timmar)**: för certifikat profiler som innehåller Simple Certificate Enrollment Protocol inställningar (SCEP) anger du en fördröjnings period för att undvika överdriven bearbetning på registrerings tjänsten för nätverks enheter (NDES). Standardvärdet är `64` timmar.  

    - **Ange schema för utvärdering av kompatibilitet för det här... profil**: Ange hur ofta klienten ska utvärdera kompatibiliteten för den här profilen. Välj ett **enkelt schema** eller konfigurera ett **anpassat schema**. Som standard är det enkla schemat varje `12` timme.

1. Välj **OK** för att stänga fönstret och skapa distributionen.

## <a name="delete-a-deployment"></a>Ta bort en distribution

Om du vill ta bort en distribution markerar du den i listan. I informations fönstret växlar du till fliken **distributioner** . Välj distributionen. Välj sedan **ta bort**på fliken **distribution** i menyfliksområdet.

> [!IMPORTANT]
> När du tar bort en VPN-profil distribution tar Configuration Manager inte bort VPN-profilen från Windows. Om du vill ta bort profilen från enheter tar du bort den manuellt.

## <a name="next-steps"></a>Nästa steg

[Övervaka Wi-Fi-och VPN-profiler](monitor-wifi-email-vpn-profiles.md)

[Övervaka certifikatprofiler](monitor-certificate-profiles.md)
