---
title: Hantera inställningar för Minska attackytan med Endpoint Security-policyer i Microsoft Intune | Microsoft Docs
description: Konfigurera och distribuera policyer för enheter du hanterar med inställningar för Endpoint Security-policyn Minska attackytan i Microsoft Intune
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
ms.openlocfilehash: 20c8cc73e8037c0f394547b64d562cf75271240c
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431455"
---
# <a name="attack-surface-reduction-policy-for-endpoint-security-in-intune"></a>Endpoint Security-policyn Minska attackytan i Intune

När du använder Defender som antivirusprogram på dina Windows 10-enheter kan du använda Intunes Endpoint Security-policy Minskning av attackytan till att hantera de här inställningarna på dina enheter.

Policyn Minskning av attackytan hjälper till att minska dina attackytor genom att minimera antalet platser där organisationen är sårbar för cyberhot och attacker. Mer information finns i [Översikt över minskning av attackytan]( https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/overview-attack-surface-reduction) i Windows Threat Protection-dokumentationen.

Du hittar Endpoint Security-policyn Minskning av attackytan under *Hantera* i noden **Endpoint Security** i [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431). Varje *profil* för minskning av attackytan hanterar inställningar för ett visst område på en Windows 10-enhet.

Visa [inställningar för Minskning av attackytan-profiler](../protect/endpoint-security-asr-profile-settings.md).

## <a name="prerequisites-for-attack-surface-reduction-profiles"></a>Förutsättningar för Minskning av attackytan-profiler

- Windows 10 eller senare
- Defender måste vara det primära antivirusprogrammet på enheten

## <a name="attack-surface-reduction-profiles"></a>Minskning av attackytan-profiler

**Windows 10-profiler**:

- **Isolering av appar och webbläsare** – hantera inställningar för Windows Defender Application Guard (Application Guard) inom ramen för Defender ATP. Application Guard hjälper dig att förhindra gamla och nyupptäckta attacker och kan isolera företagsdefinierade webbplatser som ej betrodda samtidigt som du definierar vilka webbplatser, molnresurser och interna nätverk som är betrodda.

  Läs mer i [Application Guard](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/wd-app-guard-overview) i dokumentationen för Microsoft Defender ATP.

- **Webbskydd** – webbskyddsinställningarna du kan hantera i Microsoft Defender ATP skapar ett nätverksskydd som skyddar dina datorer mot lika hot på internet. Genom integrationen med Microsoft Edge och populära webbläsare från tredje part som Chrome och Firefox stoppar Webbskydd webbhoten utan någon webbproxy och kan skydda datorer både när de är utanför kontoret och lokalt. Webbskydd stoppar åtkomsten till:
  - Nätfiskewebbplatser
  - Vektorer för skadlig kod
  - Webbplatser som utnyttjar sårbarheter
  - Webbplatser som inte är betrodda eller har dåligt rykte
  - Webbplatser du har blockerat i din egen indikatorlista.

  Läs mer om [Webbskydd](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/web-protection-overview) i dokumentationen för Microsoft Defender ATP.

- **Programkontroll** – inställningarna för programkontroll kan hjälpa dig att minska risken för säkerhetshot genom att begränsa vilka program som användarna kan köra och koden som körs i systemkärnan (kerneln). Hantera inställningar som kan blockera osignerade skript och MSI:er, och begränsa Windows PowerShell till att köras i begränsat språkläge.

  Läs mer om [Programkontroll](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control) i dokumentationen för Microsoft Defender ATP.

- **Regler för minskning av attackytan** – konfigurera inställningar för regler för minskning av attackytan som riktar sig mot skadlig kod och skadliga appar som ofta används till att infektera datorer, bland annat:
  - Körbara filer och skript som används i Office-appar eller e-post på webben som försöker ladda ned eller köra filer
  - Dolda eller på annat sätt misstänkta skript
  - Beteenden som appar inte normalt startar under dagtid. Minskning av attackytan gör att angripare har färre möjligheter att utföra attacker.

  Läs mer om [Regler för minskning av attackytan](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction) i dokumentationen för Microsoft Defender ATP.

- **Enhetskontroll** – med inställningarna för enhetskontroll kan du konfigurera enheter med en skiktad metod som skyddar flyttbara medier. Microsoft Defender ATP har flera funktioner för övervakning och kontroll som hjälper dig att förhindra att hot på obehörig kringutrustning används i angrepp på dina enheter.

  Läs mer i [Så kontrollerar du USB-enheter och andra flyttbara media med hjälp av Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/device-control/control-usb-devices-using-intune) i dokumentationen för Microsoft Defender ATP.

- **Sårbarhetsskydd** – inställningarna för sårbarhetsskydds kan skydda dig mot skadlig kod som använder sårbarheter till att infektera enheter och sprida sig. Sårbarhetsskydd består av ett antal åtgärder som kan tillämpas antingen på operativsystemnivå eller för enskilda appar.

  Läs mer om [Aktivera sårbarhetsskydd](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/enable-exploit-protection) i dokumentationen för Microsoft Defender ATP.

## <a name="next-steps"></a>Nästa steg

[Konfigurera Endpoint Security-policyer](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
