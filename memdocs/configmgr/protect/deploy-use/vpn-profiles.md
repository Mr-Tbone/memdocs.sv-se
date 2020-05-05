---
title: VPN-profiler
titleSuffix: Configuration Manager
description: Lär dig hur du använder VPN-profiler i Configuration Manager för att distribuera VPN-inställningar till användare i din organisation.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: c0f094f1-852e-4606-91db-97846d8f0772
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9463d857599e676da6267313df575c8881436f93
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722258"
---
# <a name="vpn-profiles-in-configuration-manager"></a>VPN-profiler i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

<!--1283610-->
Använd VPN-profiler i Configuration Manager för att distribuera VPN-inställningar till användare i din organisation. Genom att distribuera inställningarna gör du det enklare för slutanvändaren att ansluta till resurser i företagsnätverket.  

Till exempel vill du konfigurera alla Windows 10-enheter med de inställningar som krävs för att ansluta till en fil resurs i det interna nätverket. Skapa en VPN-profil med de inställningar som krävs för att ansluta till det interna nätverket. Distribuera sedan profilen till alla användare som har enheter som kör Windows 10. Dessa användare ser VPN-anslutningen i listan över tillgängliga nätverk och kan ansluta med liten ansträngning.

När du skapar en VPN-profil kan du inkludera ett brett utbud av säkerhets inställningar. Inställningarna omfattar certifikat för Server verifiering och klientautentisering som du etablerar med Configuration Manager certifikat profiler. Mer information finns i [certifikat profiler](introduction-to-certificate-profiles.md).

> [!Note]
> Configuration Manager aktiverar inte den här valfria funktionen som standard. Du måste aktivera den här funktionen innan du använder den. Mer information finns i avsnittet [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

## <a name="supported-platforms"></a>Plattformar som stöds

I följande tabell beskrivs de VPN-profiler som du kan konfigurera för olika enhets plattformar.

|Anslutningstyp|Windows 8,1|Windows RT|Windows RT 8.1|Windows 10|
|---------------|-----------|----------|--------------|----------|
|**Pulse Secure**|Ja|Inga|Ja|Ja|
|**F5 Edge Client**|Ja|Inga|Ja|Ja|
|**Dell SonicWALL Mobile Connect**|Ja|Inga|Ja|Ja|
|**Check Point Mobile VPN**|Ja|Inga|Ja|Ja|
|**Microsoft SSL (SSTP)**|Ja|Ja|Ja|Inga|
|**Microsoft Automatic**|Ja|Ja|Ja|Inga|
|**IKEv2**|Ja|Ja|Ja|Inga|
|**PPTP**|Ja|Ja|Ja|Inga|
|**L2TP**|Ja|Ja|Ja|Inga|

## <a name="next-step"></a>Nästa steg

> [!div class="nextstepaction"]
> [Så här skapar du VPN-profiler](create-vpn-profiles.md)

## <a name="see-also"></a>Se även

- [Krav för VPN-profiler](../plan-design/prerequisites-for-wifi-vpn-profiles.md)

- [Säkerhet och sekretess för VPN-profiler](../plan-design/security-and-privacy-for-wifi-vpn-profiles.md)
