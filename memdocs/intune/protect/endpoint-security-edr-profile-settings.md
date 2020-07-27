---
title: Endpoint Security-inställningar för Slutpunktsidentifiering och svar i Intune | Microsoft Docs
description: Inställningar för Endpoint Security-policyn Slutpunktsidentifiering och svar i Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
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
ms.openlocfilehash: e26719bb9bf322e3e4bf11b39911e98788707629
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/18/2020
ms.locfileid: "86460424"
---
# <a name="endpoint-detection-and-response-policy-settings-for-endpoint-security-in-intune"></a>Inställningar för Endpoint Security-policyn Slutpunktsidentifiering och svar i Intune

Visa de inställningar du kan konfigurera i profiler för policyn [Slutpunktsidentifiering och svar](../protect/endpoint-security-edr-policy.md) i noden Endpoint Security i Intune.

Plattformar och profiler som stöds:

- **Windows 10 och senare**: Använd den här plattformen för policyer du distribuerar till enheter som hanteras med Intune.
  - Profil: **Slutpunktsidentifiering och svar (MDM)**

- **Windows 10 och Windows Server**: Använd den här plattformen för policyer du distribuerar till enheter som hanteras av Configuration Manager.
  - Profil: **Slutpunktsidentifiering och svar (ConfigMgr)**

## <a name="endpoint-detection-and-response-mdm"></a>Slutpunktsidentifiering och svar (MDM)

**Slutpunktsidentifiering och svar**:

- **Pakettyp för konfiguration av Microsoft Defender ATP-klient**

  Ladda upp ett signerat konfigurationspaket som ska användas för registrering av Microsoft Defender ATP-klienten.

  - **Ej konfigurerat** (*standard*)
  - **Registreringsblob**  
  - **Avregistreringsblob**  

  När värdet är *Registreringsblob* kan du konfigurera följande inställningar:

  - **Registreringsblob för Advanced Threat Protection**  
    Klicka på **Välj registreringsfil** för att öppna rutan *Välj registreringsfil* där du anger en `.onboarding`-fil.

  När värdet är *Avregistreringsblob* kan du konfigurera följande inställningar:
  
  - **Avregistreringsblob för Advanced Threat Protection**  
     Klicka på **Välj avregistreringsfil** för att öppna rutan *Välj avregistreringsfil* där du anger en `.offboarding`-fil.

- **Exempeldelning för alla filer**  

  Returnerar eller anger konfigurationsparametern för exempeldelning i Microsoft Defender Avancerat skydd.  
  - **Inte konfigurerat** (*standard*)
  - **Ja**

- **Skicka frekvensvärde för telemetrirapportering**

  - **Inte konfigurerat** (*standard*)
  - **Ja** – öka frekvensen för telemetrirapportering från Microsoft Defender Advanced Threat Protection.

## <a name="endpoint-detection-and-response-configmgr"></a>Slutpunktsidentifiering och svar (ConfigMgr)

**Slutpunktsidentifiering och svar**:

- **Exempeldelning för alla filer**  

  Returnerar eller anger konfigurationsparametern för exempeldelning i Microsoft Defender Avancerat skydd.  
  - **Inte konfigurerat** (*standard*)
  - **Ja**

- **Skicka frekvensvärde för telemetrirapportering**

  - **Inte konfigurerat** (*standard*)
  - **Ja** – öka frekvensen för telemetrirapportering från Microsoft Defender Advanced Threat Protection.

## <a name="next-steps"></a>Nästa steg

[Endpoint Security-policyn EDR](../protect/endpoint-security-edr-policy.md)
