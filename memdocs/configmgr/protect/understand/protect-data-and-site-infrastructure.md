---
title: Skydda data och platsinfrastruktur
titleSuffix: Configuration Manager
description: Lär dig hur du skyddar din organisations resurser mot exponering eller skadlig attack med Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 2117f786-d521-4790-9e8d-ec096c63c9d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 381f9d190b1d73bbbab6142fd9587e881d0870ce
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723917"
---
# <a name="protect-data-and-site-infrastructure"></a>Skydda data och platsinfrastruktur

*Gäller för: Configuration Manager (aktuell gren)*

Du vill att dina användare ska ha åtkomst till organisationens resurser på ett säkert sätt. Skydda både din infrastruktur och dina data från exponering eller skadlig attack. Använd Configuration Manager för att aktivera åtkomst och skydda din organisations resurser.  

- Med [Endpoint Protection](../deploy-use/endpoint-protection.md) kan du hantera följande Microsoft Defender-principer för klient datorer:

  - Microsoft Defender program mot skadlig kod
  - Microsoft Defender-brandväggen
  - Microsoft Defender Advanced Threat Protection
  - Microsoft Defender sårbarhets skydd
  - Microsoft Defender Application Guard
  - Microsoft Defender Application Control

  > [!TIP]
  > Om du vill hantera Endpoint Protection på samhanterade Windows 10-enheter med hjälp av moln tjänsten i Microsoft Endpoint Manager, byter du [ **Endpoint Protection** arbets belastning](../../comanage/workloads.md#endpoint-protection) till Intune. Mer information finns i [Endpoint Protection för Microsoft Intune](https://docs.microsoft.com/intune/endpoint-protection-windows-10).

- Skydda data som lagras på lokala Windows-klienter med BitLocker-diskkryptering (BDE). Configuration Manager tillhandahåller fullständig livs cykel hantering i BitLocker som kan ersätta användningen av Microsoft BitLocker administration och övervakning (MBAM). Mer information finns i [Planera för BitLocker-hantering](../plan-design/bitlocker-management.md).

- I stället för traditionella lösen ord aktiverar du alternativa inloggnings metoder på Windows 10-enheter med Windows Hello för företag. Mer information finns i [Inställningar för Windows Hello för företag](../deploy-use/windows-hello-for-business-settings.md).

- Minimera användarnas ansträngningar att ansluta till resurser genom att aktivera VPN-anslutning med VPN-profiler. Mer information finns i [VPN-profiler](../deploy-use/vpn-profiles.md).  

- Wi-Fi-profiler tillhandahåller en uppsättning verktyg och resurser som hjälper dig att hantera trådlösa nätverks inställningar på enheter i din organisation. Genom att distribuera de här inställningarna minimerar du den ansträngning som slutanvändarna behöver för att ansluta till trådlösa nätverk. Mer information finns i [Wi-Fi-profiler](../deploy-use/create-wifi-profiles.md).  

- Etablera enheter med de certifikat som användarna behöver för att ansluta till resurser. Mer information finns i [certifikat profiler](../deploy-use/introduction-to-certificate-profiles.md).  
