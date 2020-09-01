---
title: Klient kopplings Configuration Manager klienter till Microsoft Defender ATP från Microsoft Endpoint Manager administrations Center (för hands version)
titleSuffix: Configuration Manager
description: Distribuera EDR-principer för hantering av Microsoft Defender ATP-identifiering och-svar () för att Configuration Manager hanterade klienter från administrations centret.
ms.date: 08/24/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 50f8e206-a2af-469a-9f1b-0f7a87166f48
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: a2862812145e33a992ceaa346e138606eee5fad0
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/31/2020
ms.locfileid: "89194220"
---
# <a name="tenant-attach-onboard-configuration-manager-clients-to-microsoft-defender-atp-from-the-admin-center-preview"></a><a name="bkmk_atp"></a> Klient anslutning: publicera Configuration Manager klienter till Microsoft Defender ATP från administrations centret (för hands version)
<!--5691658-->
*Gäller för: Configuration Manager (aktuell gren)*

> [!Important]
> Den här informationen är relaterad till en förhands gransknings funktion som kan ändras avsevärt innan den släpps kommersiellt. Microsoft lämnar inga garantier, uttryckliga eller underförstådda, avseende informationen som visas här.

Microsoft Endpoint Manager är en integrerad lösning för att hantera alla dina enheter. Microsoft sammanför Configuration Manager och Intune i en enda konsol som kallas **administrations Center för Microsoft Endpoint Manager**. Du kan distribuera EDR-principer för hantering av Microsoft Defender ATP-identifiering och-svar () för att Configuration Manager hanterade klienter. Dessa klienter kräver inte Azure AD eller MDM-registrering och principen riktas mot ConfigMgr-samlingar i stället för Azure AD-grupper.

## <a name="prerequisites"></a>Krav

- Åtkomst till [administrations centret för Microsoft Endpoint Manager](https://endpoint.microsoft.com/).
- En E5-licens för [Microsoft Defender ATP](/windows/security/threat-protection/microsoft-defender-atp/minimum-requirements#licensing-requirements).
- En miljö som är [ansluten till uppladdade enheter](device-sync-actions.md).
- Minst Configuration Manager version 2006 och motsvarande version av konsolen installerad.
   - Uppgradera mål enheterna till den senaste versionen av Configuration Manager-klienten.

## <a name="make-configuration-manager-collections-available-to-assign-endpoint-security-policies"></a><a name="bkmk_collections"></a> Gör Configuration Manager samlingar tillgängliga för att tilldela principer för slut punkts säkerhet

När du aktiverar samlingar av enheter för att arbeta med säkerhetsprinciper för slutpunkter från Intune, konfigurerar du de enheter i dessa samlingar som ska publiceras med Microsoft Defender ATP.

[!INCLUDE [Enable endpoint security policies for a Configuration Manager collection](../../intune/protect/includes/make-configmgr-collection-available-edr.md)]

## <a name="create-microsoft-defender-atp-endpoint-detection-and-response-edr-onboarding-policies"></a><a name="bkmk_onboard"></a> Skapa registrerings principer för Microsoft Defender ATP-EDR (slut punkts identifiering och svar)

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://endpoint.microsoft.com).

1. Välj **Endpoint Security** > **Slutpunktsidentifiering och svar** > **Skapa policy**.

1. Välj följande plattform och profil för principen:

   - Plattform: **Windows 10 och Windows Server (ConfigMgr)**
   - Profil: **Slutpunktsidentifiering och svar (ConfigMgr)**

1. Välj **Skapa**.

1. På sidan **Grundläggande inställningar** anger du ett namn och en beskrivning för profilen. Välj sedan **Nästa**.

1. På sidan **Konfigurationsinställningar** konfigurerar du de inställningar du vill hantera med den här profilen. Registreringspaketet ingår automatiskt och du kan inte konfigurera det.

   När du har konfigurerat inställningarna väljer du **Nästa**.

1. På sidan **tilldelningar** väljer du de samlingar som ska ta emot den här principen. Välj samlingar från Configuration Manager som du har synkroniserat med administrations Center för Microsoft Endpoint Manager och aktiverat för Microsoft Defender ATP-principen.

   Du kan välja att inte tilldela samlingar för tillfället och senare redigera principen för att lägga till en tilldelning.

   När du är redo att fortsätta väljer du **Nästa**.

1. Välj **Skapa**på sidan **Granska + skapa** när du är klar.

   Den nya profilen visas i listan när du väljer policytypen för den profil du har skapat.

## <a name="next-steps"></a>Nästa steg

[Skapa och distribuera Endpoint Security antivirus policy till anslutna klient enheter](deploy-antivirus-policy.md)