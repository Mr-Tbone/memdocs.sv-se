---
title: Vanliga frågor och svar om Microsoft Endpoint Configuration Manager
titleSuffix: Configuration Manager
description: Vanliga frågor och svar om Microsoft Endpoint Configuration Manager
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: be276b34-e283-4386-8b45-5629e431c50d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e0b59ffa73bb2c7524f2eed29326f238d856adef
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699321"
---
# <a name="microsoft-endpoint-configuration-manager-faq"></a>Vanliga frågor och svar om Microsoft Endpoint Configuration Manager

*Gäller för: Configuration Manager (aktuell gren, Technical Preview-gren)*

Från Configuration Manager och med version 1910 är nu en del av Microsoft Endpoint Manager. Den här artikeln innehåller svar på vanliga frågor.

## <a name="summary"></a>Sammanfattning

Börja med att titta på följande två minuter långa video från Brad Anderson, Microsofts vice ordförande för Microsoft 365:

> [!VIDEO https://www.youtube.com/embed/GS7oNPInFuw]

## <a name="faqs"></a>Vanliga frågor och svar

### <a name="what-is-microsoft-endpoint-manager"></a>Vad är Microsoft Endpoint Manager?

Microsoft Endpoint Manager är en integrerad lösning för att hantera alla dina enheter. Microsoft sammanför Configuration Manager och Intune med förenklad licensiering. Fortsätt att använda dina befintliga Configuration Manager-investeringar och dra nytta av kraften i Microsoft Cloud i din egen takt.

Följande Microsoft-hanterings lösningar är nu en del av **Microsoft Endpoint Manager** -varumärket:

- [Configuration Manager](/configmgr)
- [Intune](/intune)
- [Desktop Analytics](../../desktop-analytics/overview.md)
- [Autopilot](/intune/enrollment/enrollment-autopilot)
- Andra funktioner i [administrations konsolen för enhets hantering](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/microsoft-intune-rolls-out-an-improved-streamlined-endpoint/ba-p/937760)

Mer information finns i följande inlägg från Bengt Anderson, Microsoft corporate vice president för Microsoft 365:

- [Blogg inlägg i meddelande](https://aka.ms/cmannounce)
- [Syn papper](https://aka.ms/MEMVisionPaper)

### <a name="what-things-change-in-configuration-manager-with-microsoft-endpoint-manager"></a>Vad har ändrats i Configuration Manager med Microsoft Endpoint Manager?

I version 1910, bortsett från namn ändringen, Configuration Manager fungerar fortfarande på samma sätt.

I de flesta fall har mappen Start-menyns mappnamn ändrats för vanliga komponenter, till exempel [Configuration Manager-konsolen](../servers/manage/admin-console.md#bkmk_open) och [Software Center](software-center.md#bkmk_open).

### <a name="how-do-we-refer-to-the-product-now"></a>Hur refererar vi till produkten nu?

- När du refererar till hela lösningen som innehåller alla komponenter: **Microsoft Endpoint Manager**

- När du refererar till den lokala komponenten:
  - I den första referensen använder du fullständigt märkes namn: **Microsoft Endpoint Configuration Manager**
  - För allmän användning: **Configuration Manager**
  - För utrymmes begränsad användning: **ConfigMgr**, endast i instanser där namnet för allmän användning inte passar

### <a name="are-there-any-licensing-changes"></a>Finns det några licens ändringar?

Javisst! Som lanseras på Microsoft antändning 2019, om du är licensierad för Configuration Manager, licensieras du nu även för Intune för att [Hantera](../../comanage/overview.md) dina Windows-datorer. Mer information finns i [vanliga frågor och svar om produkt och licensiering](product-and-licensing-faq.md#bkmk_mem).

### <a name="why-do-i-still-see-system-center-configuration-manager-some-places"></a>Varför ser jag fortfarande "System Center Configuration Manager" några platser?

Det tar tid att göra ändringar i alla produkter, tjänster och stöd material som dokumentation.

Det finns även vissa grundläggande komponenter som kanske aldrig ändras. Huvud Windows-tjänsten på plats servrar är fortfarande **SMS_EXECUTIVE**. GitHub-lagringsplatsen som har stöd för den här dokumentationen kommer även fortsättnings vis att vara **SCCMDocs**.

## <a name="next-steps"></a>Nästa steg

Lär dig mer om [vad som är nytt i Configuration Manager stegvisa versioner](../plan-design/changes/whats-new-incremental-versions.md).