---
title: Moln anslutning med samhantering
titleSuffix: Configuration Manager
description: Samhantering ger omedelbar värde när du aktiverar det.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 8d878443-90e7-46e4-9cd3-99e2a19b2ad0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5ca960ddd6a4057da10341063f0b14a7f1d104d1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075820"
---
# <a name="cloud-connecting-with-co-management"></a>Moln anslutning med samhantering

![Banderoll för blastoff-serien](media/blastoff-banner.png)

Co-Management lägger till nya funktioner i din befintliga Configuration Manager-distribution, utan att ändra hur du redan fungerar. När du aktiverar samhantering börjar du direkt får från molnet. Du kan använda det värdet för din befintliga hanterings infrastruktur och-processer.

I den här snabb starts serien för samhantering, se hur du snabbt kan öka det nya hantering svärdet. Samhantering har skapats för att skapa funktioner och verktyg som du kan använda just nu.

I följande videoklipp introducerar Microsoft corporate vice president Bengt Anderson den här samhanterings serien:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Cloud-Connecting-with-Co-Management/player]

| Omedelbart värde | Komma igång |
|-----------------|-----------------|
| - [Villkorlig åtkomst](#bkmk_ca)<br> - [Fjärråtgärder från Intune](#bkmk_remote)<br> - [Klient hälsa](#bkmk_client-health)<br> - [Hybrid Azure AD](#bkmk_hybrid-aad)<br> - [Windows autopilot](#bkmk_autopilot) | - [Sökvägar till samhantering](#bkmk_paths)<br> - [Konfigurera hybrid Azure AD](#bkmk_setup-hybrid-aad)<br> - [Uppgradera till Windows 10](#bkmk_upgrade-win10)<br> - [Få hjälp från FastTrack](#bkmk_fasttrack) |

## <a name="immediate-value"></a>Omedelbart värde

| | | |
|-|-|-|
| <a name="bkmk_ca"></a>**Villkorlig åtkomst med enhetens efterlevnad** | Kontrol lera användarnas åtkomst till företags resurser baserat på regler för efterlevnad från Intune | [![Miniatyr av video för villkorlig åtkomst](media/thumbnail-conditional-access.png)](quickstart-conditional-access.md) |
| <a name="bkmk_remote"></a>**Fjärråtgärder från Intune** | Kör fjärråtgärder från Intune för samhanterade enheter. Du kan till exempel rensa och återställa en enhet och underhålla registrering och konto | [![Miniatyr av video för fjärråtgärder](media/thumbnail-remote-action.png)](quickstart-remote-actions.md) |
| <a name="bkmk_client-health"></a>**Configuration Manager klient hälsa** | Behåll synligheten för Configuration Manager klient hälsa från Intune på Azure Portal | [![Miniatyr av klientens hälso video](media/thumbnail-client-health.png)](quickstart-client-health.md) |
| <a name="bkmk_hybrid-aad"></a>**Azure Active Directory (Azure AD)** | Med Azure AD kan du dra nytta av förbättrad produktivitet för dina användare och säkerhet för dina resurser, i både moln-och lokal miljöer | [![Miniatyr bild av hybrid Azure AD-video](media/thumbnail-azure-ad.png)](quickstart-hybrid-aad.md) |
| <a name="bkmk_autopilot"></a>**Windows autopilot** | Minska tiden, resurserna och komplexiteten för att distribuera, hantera och dra tillbaka eller återvinna enheter. Autopiloten skapar också en bättre upplevelse för slutanvändare. | [![Miniatyr av Windows autopilot-video](media/thumbnail-autopilot.png)](quickstart-autopilot.md) |

## <a name="getting-started"></a>Komma igång

Om du vill aktivera samhantering börjar du här för att avblockera de tekniska problem som du kan ha.

| | | |
|-|-|-|
| <a name="bkmk_paths"></a>**Sökvägar till samhantering** | Det finns två huvudsakliga sätt att konfigurera samhantering, och det är viktigt att förstå kraven för varje sökväg.  Varje sökväg kräver viss kombination av Azure AD-, ConfigMgr-, Intune-och Windows-klient. | [![Miniatyr bild av bilden med samhanterings Sök vägar](media/thumbnail-paths.png)](quickstart-paths.md) |
| <a name="bkmk_setup-hybrid-aad"></a>**Konfigurera hybrid Azure AD** | Om din miljö för närvarande har domänanslutna Windows 10-enheter konfigurerar du hybrid Azure AD innan du kan aktivera samhantering | [![Miniatyr bild av konfiguration av hybrid Azure AD-video](media/thumbnail-setup-azure-ad.png)](quickstart-setup-hybrid-aad.md) |
| <a name="bkmk_upgrade-win10"></a>**Uppgradera till Windows 10** | Windows 10 version 1709 eller senare krävs för samtidig hantering | [![Miniatyr bild av uppgradering av Windows 10-video](media/thumbnail-upgrade-win10.png)](quickstart-upgrade-win10.md) |
| <a name="bkmk_fasttrack"></a>**Få hjälp från FastTrack** | FastTrack-organisationen är en stor grupp Microsoft-tekniker som specialiserar sig på att hjälpa alla typer av organisationer att distribuera Microsoft 365 appar, inklusive att konfigurera samhantering. | [![Miniatyr av FastTrack-videon](media/thumbnail-fasttrack.png)](quickstart-fasttrack.md) |
