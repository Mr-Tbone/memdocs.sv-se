---
title: Klient koppling – distribuera slut punkts säkerhets Antivirus princip från administrations Center för Microsoft Endpoint Manager (för hands version)
titleSuffix: Configuration Manager
description: " Skapa och distribuera Microsoft Defender Antivirus-principer från Microsoft Endpoint Manager-konsolen och för Configuration Manager samlingar."
ms.date: 08/24/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 07379821-02b3-4c61-af03-329c782e10d6
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: d09b519bfc116afd397d455c6a03a8748f9303cd
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/25/2020
ms.locfileid: "88827032"
---
# <a name="tenant-attach-create-and-deploy-endpoint-security-antivirus-policy-from-the-admin-center-preview"></a><a name="bkmk_atp"></a> Klient anslutning: skapa och distribuera slut punkts säkerhets Antivirus princip från administrations Center (för hands version)
<!--5691658-->
*Gäller för: Configuration Manager (aktuell gren)*

> [!Important]
> Den här informationen är relaterad till en förhands gransknings funktion som kan ändras avsevärt innan den släpps kommersiellt. Microsoft lämnar inga garantier, uttryckliga eller underförstådda, avseende informationen som visas här. 

Microsoft Endpoint Manager är en integrerad lösning för att hantera alla dina enheter. Microsoft sammanför Configuration Manager och Intune i en enda konsol som kallas **administrations Center för Microsoft Endpoint Manager**. Skapa Microsoft Defender Antivirus-principer i Microsoft Endpoint Manager-konsolen och distribuera dem till Configuration Manager samlingar.


## <a name="prerequisites"></a>Förutsättningar

- Åtkomst till [administrations centret för Microsoft Endpoint Manager](https://endpoint.microsoft.com/).
- En E5-licens för [Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/minimum-requirements#licensing-requirements).
- En miljö som är [ansluten till uppladdade enheter](device-sync-actions.md).
- Minst Configuration Manager version 2006 och motsvarande version av konsolen installerad.
   - Uppgradera mål enheterna till den senaste versionen av Configuration Manager-klienten.
- Minst en Configuration Manager samling som är [tillgänglig för tilldelning av slut punkts säkerhets principer](atp-onboard.md#bkmk_collections)

## <a name="supported-antivirus-profile-for-tenant-attached-devices"></a>Antivirus profil som stöds för anslutna klient enheter

[!INCLUDE [Profiles for Configuration Manager tenant attached devices](../../intune/protect/includes/configmgr-antivirus-profiles.md)]

## <a name="assign-antivirus-policies-to-a-collection"></a>Tilldela Antivirus principer till en samling

1. Gå till i en webbläsare [https://aka.ms/MDAVTenantAttachPreview](https://aka.ms/MDAVTenantAttachPreview) .
1. Välj **slut punkts säkerhet** och sedan **Antivirus**.
1. Välj **Skapa princip**.
1. För **plattformen**väljer du **Windows 10 och Windows Server (ConfigMgr)**.
1. För **profilen**väljer du **Microsoft Defender Antivirus (för hands version)** och sedan **skapa**.
1. Ange ett **namn** och eventuellt en **Beskrivning** på sidan **grundläggande** .
1. På sidan **Konfigurationsinställningar** konfigurerar du de inställningar du vill hantera med den här profilen. När du har konfigurerat inställningarna väljer du **Nästa**. Mer information om tillgängliga principer finns i [Inställningar för Antivirus principer för anslutna klient enheter](../../intune/protect/antivirus-microsoft-defender-settings-windows-tenant-attach.md?toc=/mem/configmgr/tenant-attach/toc.json&bc=/mem/configmgr/tenant-attach/breadcrumb/toc.json).
1. Tilldela principen till en Configuration Manager-samling på sidan **tilldelningar** .

## <a name="next-steps"></a>Nästa steg

[Antivirus princip inställningar för anslutna klient enheter](../../intune/protect/antivirus-microsoft-defender-settings-windows-tenant-attach.md?toc=/mem/configmgr/tenant-attach/toc.json&bc=/mem/configmgr/tenant-attach/breadcrumb/toc.json)