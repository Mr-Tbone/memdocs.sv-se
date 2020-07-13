---
title: Hantera brandväggsinställningar med Endpoint Security-policyer i Microsoft Intune | Microsoft Docs
description: Konfigurera och distribuera policyer för enheter du hanterar med Endpoint Security-policyn Brandvägg i Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/15/2020
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
ms.openlocfilehash: 5b33be56975713c801d2ad3fdea17e6303687274
ms.sourcegitcommit: 03d2331876ad61d0a6bb1efca3aa655b88f73119
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/03/2020
ms.locfileid: "85946920"
---
# <a name="firewall-policy-for-endpoint-security-in-intune"></a>Endpoint Security-policyn Brandvägg i Intune

Använd Endpoint Security-policyn Brandvägg i Intune till att konfigurera den inbyggda brandväggen för enheter som kör macOS och Windows 10.

Även om du kan konfigurera samma brandväggsinställningar genom att använda Endpoint Security-profiler för enhetskonfiguration så innehåller enhetskonfigurationsprofilerna ytterligare inställningskategorier. De ytterligare inställningarna gäller inte brandväggar och kan göra det krångligare att konfigurera brandväggsinställningar för din miljö.

Du hittar Endpoint Security-policyn Brandvägg under *Hantera* i noden **Endpoint Security** i [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

Visa [inställningar för brandväggsprofiler](../protect/endpoint-security-Firewall-profile-settings.md).

## <a name="prerequisites-for-firewall-profiles"></a>Förutsättningar för brandväggsprofiler

- Windows 10 eller senare
- En version av macOS som stöds

## <a name="firewall-profiles"></a>Brandväggsprofiler

**macOS-profiler**:

- **macOS-brandvägg** – aktivera och konfigurera inställningar för den inbyggda brandväggen i macOS.

**Windows 10-profiler**:

- **Microsoft Defender-brandväggen** – konfigurera inställningar för Windows Defender-brandväggen med avancerad säkerhet. Windows Defender-brandväggen ger värdbaserad, dubbelriktad filtrering av nätverkstrafik för en enhet och kan blockera obehörig nätverkstrafik som flödar in till eller ut från den lokala enheten.

- **Microsoft Defender-brandväggsregler** *(förhandsversion)* – definiera detaljerade brandväggsregler med specifika portar, protokoll, program och nätverk för att tillåta eller blockera nätverkstrafik. Varje instans av den här profilen har stöd för upp till 150 anpassade regler.

## <a name="firewall-rule-mergers-and-policy-conflicts"></a>Sammanslagning av brandväggsregler och policykonflikter

Planera för tillämpning av brandväggspolicyer så att bara en policy används på enheten. Om du bara använder en policyinstans och policytyp undviker du att två separata policyer tillämpar olika konfigurationer för samma inställning, vilket skapar en konflikt. När det finns en konflikt mellan två policyinstanser eller policytyper som hanterar samma inställning med olika värden skickas inte inställningen till enheten.

- Den här typen av policykonflikt gäller för **Microsoft Defender-brandväggsprofilen**, som kan vara i konflikt med andra Microsoft Defender-brandväggsprofilen eller en brandväggskonfiguration som levereras via en annan policytyp som en enhetskonfiguration.

  *Microsoft Defender-brandväggsprofiler* hamnar inte i konflikt med *Microsoft Defender-brandväggsregelprofiler*.

När du använder **Microsoft Defender-brandväggsregelprofiler** kan du tillämpa flera regelprofiler på samma enhet. Men när det finns olika regler för samma sak med olika konfigurationer skickas båda till enheten och skapar en konflikt på enheten.

- Om en regel till exempel blockerar *Teams.exe* genom brandväggen och en andra regel tillåter *Teams.exe* så levereras båda reglerna till klienten. Resultatet är inte som vid andra konflikter som uppstår med andra policyer för brandväggsinställningar.

När regler från flera regelprofiler inte står i konflikt med varandra sammanfogar enheterna reglerna från varje profil och skapar en kombinerad regelkonfiguration för brandväggen på enheten. Det här beteendet gör att du kan distribuera fler än de 150 regler som varje enskild profil har stöd för till en enhet.

- Du kan till exempel ha två Microsoft Defender-brandväggsregelprofiler. Den första profilen tillåter *Teams.exe* genom brandväggen. Den andra profilen tillåter *Outlook.exe* genom brandväggen. När en enhet tar emot båda profilerna är enheten konfigurerad för att tillåta båda apparna genom brandväggen.

## <a name="next-steps"></a>Nästa steg

[Konfigurera Endpoint Security-policyer](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
