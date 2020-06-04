---
title: Principinställningar för kontoskydd i Intunes slutpunktssäkerhet | Microsoft Docs
description: Principinställningar för Endpoint Security-kontoskydd i Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/17/2020
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
ms.openlocfilehash: f4e67c434af9eb7f88c3e7d3997ef7c7d829c860
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/15/2020
ms.locfileid: "83432001"
---
# <a name="account-protection-policy-settings-for-endpoint-security-in-intune"></a>Inställningar för kontoskyddspolicy för slutpunktssäkerhet i Intune

Visa de inställningar du kan konfigurera i profiler för principen *Kontoskydd* i noden Slutpunktssäkerhet i Intune inom ramen för [policyn Slutpunktssäkerhet](../protect/endpoint-security-policy.md).

Plattformar och profiler som stöds:

- **Windows 10 och senare**:
  - Profil: **Kontoskydd**  *(förhandsversion)*


## <a name="account-protection-profile"></a>Profil för kontoskydd

### <a name="account-protection"></a>Kontoskydd

- **Blockera Windows Hello för företag**

  Windows Hello för företag är en alternativ metod för att logga in till Windows genom att ersätta lösenord, smartkort och virtuella smartkort.
  - **Inte konfigurerad**  (*standard*) – Enheter etablerar Windows Hello för företag.
  - **Inaktiverad** – Enheter etablerar Windows Hello för företag.
  - **Aktiverad** – Enheter etablerar inte Windows Hello för företag för någon användare
  
- **Aktivera användning av säkerhetsnycklar för inloggning**

  Aktivera säkerhetsnyckeln för Windows Hello som inloggningsinformation för alla datorer i klientorganisationen.
  - **Ej konfigurerat** (*standard*)
  - **Ja**

- **Aktivera Credential Guard**  
  [CSP: []DeviceGuard](https://go.microsoft.com/fwlink/?linkid=872424)

  Credential Guard använder Windows Hypervisor för att ge skydd. Credential Guard kräver maskinvarustöd för Säker start och DMA-skydd. Den här inställningen fungerar bara på enheter som uppfyller maskinvarukraven.
  - **Inte konfigurerat** (*standard*) – Inaktivera användningen av Credential Guard, som är Windows-standard.
  - **Aktivera med UEFI-lås** – Aktivera Credential Guard och blockera att det kan stängas av via fjärranslutning, eftersom den kvarstående konfigurationen i UEFI måste rensas manuellt.
  - **Aktivera utan UEFI-lås** – Aktivera Credential Guard och tillåt att det inaktiveras utan fysisk åtkomst till datorn.

## <a name="next-steps"></a>Nästa steg

[Säkerhetsprincip för slutpunkt för kontoskydd](../protect/endpoint-security-account-protection-policy.md)
