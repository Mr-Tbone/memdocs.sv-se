---
title: Hantera inställningar för diskkryptering med principer för Endpoint Security i Microsoft Intune | Microsoft Docs
description: Konfigurera och distribuera principer för enheter du hanterar med säkerhetsprinciper för diskkryptering i Microsoft Endpoint Manager.
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
ms.openlocfilehash: b988e4ddeb306c7da290c87e8a32fa0571627257
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431676"
---
# <a name="disk-encryption-policy-for-endpoint-security-in-intune"></a>Principer för diskkryptering i Intunes slutpunktssäkerhet

Diskkrypteringsprofilerna för slutpunktssäkerhet fokuserar bara på de inställningar som är relevanta för enheters inbyggda krypteringsmetod, som FileVault eller BitLocker. Det här gör att säkerhetsadministratörer enklare kan hantera diskkrypteringsinställningar utan att behöva navigera bland en massa irrelevanta inställningar.

Även om du kan konfigurera samma enhetsinställningar genom att använda profiler för *Endpoint Protection* för enhetskonfiguration, innehåller enhetskonfigurationsprofilerna ytterligare inställningskategorier. Dessa ytterligare inställningar är inte relaterade till diskkryptering och kan komplicera uppgiften att bara konfigurera diskkryptering.

Hitta principerna för slutpunktssäkerhet för diskkrypteringsprinciper under *Hantera* i noden **Slutpunktssäkerhet** i [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

## <a name="prerequisites-for-disk-encryption-policy"></a>Krav för diskkrypteringsprincip

- **macOS** – macOS 10.13 eller senare
- **Windows** – Windows 10 eller senare

## <a name="disk-encryption-profiles"></a>Profiler för diskkryptering

**macOS-profiler**:

- **FileVault** – FileVault tillhandahåller inbyggd fullständig diskkryptering för macOS-enheter.

  Hantera [FileVault-inställningar](../protect/endpoint-security-disk-encryption-profile-settings.md#filevault) för macOS.

  Du kan läsa mer om hur du skapar en FileVault-profil i [Use FileVault disk encryption for macOS](../protect/encrypt-devices-filevault.md) (Använda FileVault-diskkryptering för macOS).

**Windows 10-profiler**:

- **BitLocker** – BitLocker-diskkryptering är en dataskyddsfunktion som är integrerad med operativsystemet och hanterar hot om datastöld eller exponering från förlorade, stulna eller felaktigt inaktiverade datorer

  Hantera [BitLocker-inställningar](../protect/endpoint-security-disk-encryption-profile-settings.md#bitlocker) för Windows 10.

  Information om hur du skapar en BitLocker-profil finns i [Use BitLocker disk encryption for Windows 10](../protect/encrypt-devices.md) (Använda BitLocker-diskkryptering för Windows 10).

## <a name="manage-device-encryption"></a>Hantera enhetskryptering

När du har distribuerat principen för att kryptera en enhetsdisk kan du läsa följande artiklar om hur du hanterar kryptering:

- [Hantera BitLocker](../protect/encrypt-devices.md#manage-bitlocker)
- [Hantera FileVault](../protect/encrypt-devices-filevault.md#manage-filevault)
- [Övervaka enhetskryptering](../protect/encryption-monitor.md)

## <a name="next-steps"></a>Nästa steg

- [Så här skapar du en FileVault-profil](../protect/encrypt-devices-filevault.md#create-an-endpoint-security-policy-for-filevault)
- [Så här skapar du en BitLocker-profil](../protect/encrypt-devices.md#create-an-endpoint-security-policy-for-bitlocker)
