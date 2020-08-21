---
title: Vad har hänt med hybrid-MDM?
titleSuffix: Configuration Manager
description: Lär dig mer om utfasningen av hybrid hantering av mobila enheter (MDM) i Configuration Manager
ms.date: 12/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e9e0da6d-bd5a-48d9-930a-e74b34b9286c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 95ac4160895394eb075589ed18a317923f317b45
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695400"
---
# <a name="what-happened-to-hybrid-mdm"></a>Vad har hänt med hybrid-MDM?

*Gäller för: Configuration Manager (aktuell gren)*

> [!WARNING]
> Microsoft har dragit tillbaka hybrid MDM-tjänstens erbjudande från den 1 september 2019. Eventuella kvarvarande hybrid MDM-enheter tar inte emot principer, appar eller säkerhets uppdateringar.

## <a name="remove-hybrid-mdm"></a>Ta bort hybrid MDM

Om din Configuration Manager plats hade en Microsoft Intune-prenumeration måste du ta bort den.

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen. Expandera **Cloud Services**och välj noden **Microsoft Intune prenumeration** . Ta bort din befintliga Intune-prenumeration.

1. I **guiden ta bort Microsoft Intune-prenumeration**väljer du alternativet för att **ta bort Microsoft Intune-prenumerationen från Configuration Manager**och klickar sedan på **Nästa**.

1. Slutför guiden.

## <a name="deprecation-announcement"></a>Meddelande om utfasning

Följande meddelande är det ursprungliga utfasnings meddelandet:

> [!NOTE]  
> Från den 14 augusti 2018 är hybrid hantering av mobila enheter en [föråldrad funktion](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md). Från och med 1902 Intune Service Release, förväntades i slutet av februari 2019, kan nya kunder inte skapa en ny hybrid anslutning.
> <!--Intune feature 2683117-->  
> Sedan det lanseras på Azure för ett år sedan har Intune lagt till hundratals nya kundbegärda och marknads ledande tjänst funktioner. Den erbjuder nu mycket fler funktioner än de som erbjuds via hybrid hantering av mobila enheter (MDM). Intune på Azure ger en mer integrerad och strömlinjeformad administrativ upplevelse för dina företags mobilitets behov.
>
> Därför väljer de flesta kunder Intune på Azure över hybrid MDM. Antalet kunder som använder hybrid MDM fortsätter att minska när fler kunder flyttas till molnet. Från och med den 1 september 2019 kommer Microsoft att dra tillbaka hybrid MDM-tjänst erbjudandet.
>
> Den här ändringen påverkar inte lokala Configuration Manager eller [samhantering för Windows 10-enheter](../../comanage/overview.md). Om du är osäker på om du använder hybrid MDM går du till arbets ytan **Administration** i Configuration Managers konsolen, expanderar **Cloud Services**och väljer **Microsoft Intune prenumerationer**. Om du har konfigurerat en Microsoft Intune-prenumeration konfigureras din klient organisation för Hybrid MDM.
>
> **Hur påverkar det här mig?**
>
> - Microsoft kommer att stödja din hybrid MDM-användning för nästa år. Funktionen kommer även fortsättnings vis att få viktiga fel korrigeringar. Microsoft kommer att stödja befintliga funktioner på nya OS-versioner, till exempel registrering på iOS 12. Det kommer inte att finnas några nya funktioner för Hybrid MDM.  
>
> - Om du migrerar till Intune på Azure före slutet av hybrid MDM-erbjudandet bör det inte påverka slutanvändaren.  
>
> - Den 1 september 2019 kommer eventuella kvarvarande hybrid MDM-enheter inte längre att ta emot principer, appar eller säkerhets uppdateringar.  
>
> - Licensieringen är oförändrad. Intune på Azure-licenser ingår i hybrid MDM.  
>
> - Den lokala MDM-funktionen i Configuration Manager är inte föråldrad. Från och med Configuration Manager version 1810 kan du använda lokal MDM utan Intune-anslutning. Mer information finns i [en Intune-anslutning krävs inte längre för nya lokala MDM-distributioner](../../core/plan-design/changes/whats-new-in-version-1810.md#bkmk_opmdm).
>
> - Den lokala villkorliga åtkomst funktionen i Configuration Manager är också föråldrad med hybrid MDM. Om du använder villkorlig åtkomst på enheter som hanteras med Configuration Manager-klienten kontrollerar du att de är skyddade innan du migrerar.
>     1. Konfigurera principer för villkorlig åtkomst i Azure
>     2. Konfigurera efterlevnadsprinciper i Intune-portalen
>     3. Avsluta hybrid migrering och ange MDM-utfärdaren till Intune
>     4. Aktivera samhantering
>     5. Flytta arbets belastningen för hantering av efterlevnadsprinciper till Intune
>
>     Mer information finns i [villkorlig åtkomst med samhantering](../../comanage/quickstart-conditional-access.md).
>
> **Vad kan jag göra för att förbereda mig för den här ändringen?**
>
> - Börja planera migreringen för MDM från ConfigMgr-konsolen till Azure. Många kunder, inklusive Microsoft IT, har gått igenom den här processen. Mer information finns i den här fallstudien för [Microsoft](https://aka.ms/Intune_MSFT).  
>
> - Kontakta din partner av Record eller FastTrack för att få hjälp. [FastTrack för Microsoft 365](https://aka.ms/hybrid_fasttrack) kan under lätta migreringen från hybrid MDM till Intune på Azure.
>
> Mer information finns i [blogg inlägget om Intune-support](https://aka.ms/hybrid_notification).

## <a name="next-steps"></a>Nästa steg

Mer information om vilka funktioner som stöds för att hantera MDM-enheter finns i följande artiklar:

- [Vad är Microsoft Intune?](/intune/what-is-intune)
- [Vad är lokal MDM?](manage-mobile-devices-with-on-premises-infrastructure.md)
- [Enhetshantering med Exchange](../deploy-use/manage-mobile-devices-with-exchange-activesync.md)