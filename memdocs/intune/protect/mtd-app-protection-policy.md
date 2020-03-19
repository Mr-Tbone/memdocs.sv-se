---
title: Skapa en Mobile Threat Defense-appskyddsprincip (MTD) med Intune
titleSuffix: Microsoft Intune
description: Skapa en Mobile Threat Defense-appskyddsprincip (MTD) med Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 02/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0fc25aa915762e0e1df9446c9fb14513bdf20352
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79351571"
---
# <a name="create-mobile-threat-defense-app-protection-policy-with-intune"></a>Skapa en Mobile Threat Defense-appskyddsprincip med Intune

Intune med Mobile Threat Defense (MTD) hjälper dig att identifiera hot och bedöma risker på mobila enheter. Du kan skapa en Intune-appskyddsprincip som bedömer risk för att avgöra huruvida enheten tillåts att få åtkomst till företagsdata.

> [!NOTE]
> Den här artikeln gäller för alla Mobile Threat Defense-partner som har stöd för appskyddsprinciper:
>
> - Better Mobile (Android, iOS/iPadOS)
> - Zimperium (Android, iOS/iPadOS)
> - Lookout for Work (Android, iOS/iPadOS).

## <a name="before-you-begin"></a>Innan du börjar

Som en del av MTD-installationen skapade du i MTD-partnerkonsolen en princip som klassificerar olika hot i kategorierna Hög, Medel och Låg. Du måste nu ange Mobile Threat Defense-nivån i Intune-appskyddsprincipen.

Förutsättningar för appskyddsprincip med MTD:

- Konfigurera MTD-integrering med Intune. Utan den här integrationen har MTD-appskyddsprincipen ingen verkan.

## <a name="to-create-an-mtd-app-protection-policy"></a>Så här skapar du en MTD-appskyddsprincip

Använd proceduren för att [skapa en appskyddsprincip för antingen iOS/iPad eller Android](../apps/app-protection-policies.md#app-protection-policies-for-iosipados-and-android-apps) och använd följande information på sidorna *Appar*, *Villkorlig start* och *Tilldelningar*:

- **Appar**: Välj de appar som du vill ska omfattas av appskyddsprinciperna. För den här funktionsuppsättningen blockeras eller rensas apparna selektivt, baserat på enhetens riskbedömning från din valda leverantör av skydd mot mobilhot.
- **Villkorlig start**:  Under *Enhetsvillkor* använder du listrutan för att välja **Högsta tillåtna hotnivå för enhet**.

  Alternativ för hotnivån **Värde**:

  - **Skyddad**: Den här nivån är säkrast. Enheten får inte ha några existerande hot och ska ha tillgång till företagsresurser. Om något hot identifieras på enheten kommer den att utvärderas som icke-kompatibel.
  - **Låg**: Enheten följer standard om det enbart finns hot på den låga nivån på enheten. Om hot på en högre nivå identifieras får enheten statusen icke-kompatibel.
  - **Medel**: Enheten följer standard om hoten som hittas på enheten är låga eller medelhöga. Om hot på en högre nivå identifieras på enheten får den statusen icke-kompatibel.
  - **Hög**: Denna nivå är den minst säkra. Den tillåter alla hotnivåer och använder endast Mobile Threat Defense i rapporteringssyfte. Enheterna måste ha MTD-appen aktiverad med den här inställningen.

  Alternativ för **åtgärd**:

  - **Blockera åtkomst**
  - **Rensa data**

- **Tilldelningar**: Tilldela principen till användargrupper.  De enheter som används av medlemmarna i gruppen utvärderas för åtkomst till företagsdata i riktade appar via Intune-appskydd.

## <a name="next-steps"></a>Nästa steg

- Lär dig mer om [Mobile Threat Defense](mobile-threat-defense.md) i Microsoft Intune.
