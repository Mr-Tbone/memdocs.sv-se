---
title: Skapa en princip för Mobile Threat Defense-enhetsefterlevnad (MTD) med Microsoft Intune
titleSuffix: Microsoft Intune
description: Skapa en Intune-princip för enhetsefterlevnad som använder din MTD-partners hotnivåer för att bestämma om en mobil enhet ska få åtkomst till företagets resurser.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/28/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5d12254f-ffab-4792-b19c-ab37f5e02f35
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 265b92229d687c7dafb2c6de196990c29ffc0cb8
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996103"
---
# <a name="create-mobile-threat-defense-mtd-device-compliance-policy-with-intune"></a>Skapa en princip för Mobile Threat Defense-enhetsefterlevnad med Intune

Intune med MTD hjälper dig att identifiera hot och bedöma risker på mobila enheter. Du kan skapa en Intune-principregel för enhetsefterlevnad som bedömer risken och avgör om enheten uppfyller efterlevnadskraven. Du kan sedan använda en [princip för villkorlig åtkomst](create-conditional-access-intune.md) för att blockera åtkomst till tjänster utifrån enhetens efterlevnad.

> [!NOTE]
> Denna information gäller alla partners för skydd mot mobilhot.

## <a name="before-you-begin"></a>Innan du börjar

Som en del av MTD-installationen skapade du i MTD-partnerkonsolen en princip som klassificerar olika hot i kategorierna Hög, Medel och Låg. Därefter måste du ange MTD-nivå i Intune-principen för enhetsefterlevnad.

Förutsättningar för principen för enhetsefterlevnad med MTD:

- Ställ in MTD-integrering med Intune

## <a name="to-create-an-mtd-device-compliance-policy"></a>Skapa en MTD-enhetsefterlevnadsprincip

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Välj **Slutpunktssäkerhet** > **Enhetsefterlevnad** > **Skapa princip**.

3. Välj **Plattform** och sedan **Skapa**.

4. Gå till **Grundläggande inställningar** och ange en princip för enhetsefterlevnad, **Namn**och **Beskrivning** (valfritt). Fortsätt genom att välja **Nästa**.


5. Utöka och konfigurera **Enhetens hälsotillstånd** på **Kompatibilitetsinställningar**. Välj mobilhotnivå i listrutan under **Kräv att enheten ska hållas vid eller under hotnivån för enheten**.

   - **Skyddad**: Den här nivån är säkrast. Enheten får inte ha några existerande hot och ska ha tillgång till företagsresurser. Om något hot identifieras på enheten kommer den att utvärderas som icke-kompatibel.

   - **Låg**: Enheten följer standard om det enbart finns hot på den låga nivån på enheten. Om hot på en högre nivå identifieras får enheten statusen icke-kompatibel.

   - **Medel**: Enheten följer standard om hoten som hittas på enheten är låga eller medelhöga. Om hot på en högre nivå identifieras på enheten får den statusen icke-kompatibel.

   - **Hög**: Den här hotnivån är den minst säkra eftersom den tillåter alla hotnivåer och endast använder Mobile Threat Defense i rapporteringssyfte. Enheterna måste ha MTD-appen aktiverad med den här inställningen.

6. Välj **Nästa** och gå vidare till **Tilldelningar**. Välj de grupper som profilen ska tillämpas på. Mer information om hur du tilldelar profiler finns i [Tilldela användar- och enhetsprofiler](../configuration/device-profile-assign.md).

   Välj **Nästa**.

7. Välj **Skapa**på sidan **Granska + skapa** när du är klar. Den nya profilen visas i listan när du väljer policytypen för den profil du har skapat.

> [!IMPORTANT]
> Om du skapar principer för villkorsstyrd åtkomst för Microsoft 365 eller andra tjänster kommer utvärderingen av efterlevnad att bedömas och icke-kompatibla enheter kommer inte att få åtkomst till företagsresurser förrän hotet har lösts på enheten.

## <a name="to-assign-an-mtd-device-compliance-policy"></a>Tilldela en MTD-enhetsefterlevnadsprincip

Tilldela eller ändra tilldelningen av en princip för enhetsefterlevnad till användare:

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Välj **Slutpunktssäkerhet** > **Enhetsefterlevnad**.

3. Välj den princip som du vill tilldela till användarna och välj sedan **Egenskaper**.

4. Välj **Redigera** för tilldelningar och använd sedan de tillgängliga alternativen för att *inkludera* och *exkludera* vilka grupper som ska få ta emot den här principen.  

5. Slutför tilldelningen genom att välja **Granska och spara**. När du sparar tilldelningen, distribueras principen till de valda användarna och efterlevnaden utvärderas i deras enheter.

## <a name="next-steps"></a>Nästa steg

[Aktivera MTD med Intune](mtd-connector-enable.md)
