---
title: Hantera inställningar för kontoskydd mot attacker med Endpoint Security-policyer i Microsoft Intune | Microsoft Docs
description: Konfigurera och distribuera policyer för enheter du hanterar med inställningar för Endpoint Security-policyn Kontoskydd i Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: f08282fe6bd8675474415290d50c0b07b4e1fc25
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915066"
---
# <a name="account-protection-policy-for-endpoint-security-in-intune"></a>Endpoint Security-policyn Kontoskydd i Intune

Använd Endpoint Security-policyer i Intune som Kontoskydd till att skydda användarnas identiteter och konton. Kontoskyddspolicyns fokus är inställningar för Windows Hello och Credential Guard som ingår i Windows hantering av identiteter och åtkomst.

- *Windows Hello for Business* ersätter lösenord med stark tvåfaktorsautentisering på datorer och mobila enheter.
- *Credential Guard* skyddar autentiseringsuppgifter och hemligheter som du använder med dina enheter.

Läs mer i [Identity and access management](/windows/security/identity-protection/), dokumentationen om Windows hantering av identiteter och åtkomst.

Du hittar Endpoint Security-policyn Kontoskydd under *Hantera* i noden **Endpoint Security** i [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

Visa [inställningar för kontoskyddsprofiler](../protect/endpoint-security-asr-profile-settings.md).

## <a name="prerequisites-for-account-protection-profiles"></a>Förutsättningar för kontoskyddsprofiler

- Windows 10 eller senare

## <a name="account-protection-profiles"></a>Kontoskyddsprofiler

*Kontoskyddsprofiler finns i förhandsversion*.

**Windows 10-profiler**:

- **Kontoskydd** *(förhandsversion)* – inställningar för kontoskyddspolicyer som hjälper dig att skydda användarnas autentiseringsuppgifter.

## <a name="next-steps"></a>Nästa steg

[Konfigurera Endpoint Security-policyer](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)