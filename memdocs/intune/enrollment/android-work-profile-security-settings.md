---
title: Säkerhetskonfiguration för ramverk för Android Enterprise
titleSuffix: Microsoft Intune
description: Läs om de begränsningar och inställningar som föreslås för grundläggande och hög säkerhet för Android Enterprise-enheter.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/24/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: rosssmi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 23d8b972be753da2ff0c2c75d839e5a5a7e8b077
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.contentlocale: sv-SE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85503036"
---
# <a name="android-enterprise-work-profile-security-configurations"></a>Säkerhetskonfigurationer för Android Enterprise-arbetsprofiler

Som en del av [säkerhetskonfigurationsramverket för Android Enterprise](android-configuration-framework.md)använder du följande inställningar för mobila användare av Android Enterprise-arbetsprofilen. Mer information om varje principinställning finns i [Android Enterprise-inställningar för att markera enheter som kompatibla eller inte kompatibla med Intune](../protect/compliance-policy-create-android-for-work.md#work-profile) och [Android Enterprise-enhetsinställningarna för att tillåta eller begränsa funktioner med Intune](../configuration/device-restrictions-android-for-work.md#work-profile-only).

När du väljer inställningarna måste du granska och kategorisera användningsscenarier. Konfigurera sedan användare enligt riktlinjerna för den valda säkerhetsnivån. Du kan justera de föreslagna inställningarna utifrån organisationens behov. Se till att ditt säkerhetsteam utvärderar hotmiljön, riskbenägenhet och inverkan på användbarhet.

För personligt ägda arbetsprofilsenheter finns det två rekommenderade ramverk för säkerhetskonfiguration:

- [Grundläggande säkerhet för arbetsprofiler (nivå 1)](#work-profile-basic-security) 
- [Hög säkerhet för arbetsprofil (nivå 3)](#work-profile-high-security) 

> [!Note]
> På grund av inställningarna som finns tillgängliga för Android Enterprise-arbetsprofilenheter finns det inget utökat säkerhetserbjudande (nivå 2). De tillgängliga inställningarna motiverar inte en skillnad mellan nivå 1 och nivå 2.

## <a name="work-profile-basic-security"></a>Grundläggande säkerhet för arbetsprofiler

Nivå 1 är den rekommenderade minsta säkerhetskonfigurationen för personliga enheter där användare får åtkomst till arbets- eller skoldata. Den här konfigurationen kan gälla för de flesta mobila användare. Vissa av kontrollerna kan påverka användarupplevelsen.

### <a name="device-compliance"></a>Efterlevnad för enhet

| Avsnitt | Inställningen | Värde | Obs! |
| ----- | ----- | ----- | ----- |
| Microsoft Defender ATP | Kräv att enheten ska hållas vid eller under riskpoängen | Inte konfigurerat ||
| Enhetens hälsotillstånd | Rotade enheter | Blockera ||
| Enhetens hälsotillstånd | Kräv att enheten hålls på eller under enhetshotnivån | Inte konfigurerat||
| Enhetens hälsotillstånd | Google Play-tjänster har konfigurerats | Kräver ||
| Enhetens hälsotillstånd | Uppdaterad säkerhetsprovider | Kräver ||
| Enhetens hälsotillstånd | SafetyNet-enhetsattestering | Kontrollera grundläggande integritet och certifierade enheter | Den här inställningen konfigurerar Googles SafetyNet-attestering för slutanvändarenheter. Grundläggande integritet kontrollerar enhetens integritet. Rotade enheter, emulatorer, virtuella enheter och enheter med tecken på manipulation misslyckas med grundläggande integritet.<p>Grundläggande integritet och certifierade enheter validerar enhetens kompatibilitet med Googles tjänster. Endast oförändrade enheter som har certifierats av Google kan godkännas av den här kontrollen. |
| Egenskaper för enhet | Lägsta version av operativsystemet | Format: Major.Minor<br>Exempel: 5.0| Microsoft rekommenderar att du konfigurerar den lägsta Android-huvudversionen så att den matchar de Android-versioner som stöds för Microsoft-appar. OEM-tillverkare och enheter som följer rekommenderade krav för Android Enterprise måste ha stöd för den aktuella leveransversionen plus en bokstavsuppgradering. För närvarande rekommenderar Android 8.0 och senare för kunskapsarbetare. De senaste rekommendationerna för Android finns i [Rekommenderade krav för Android Enterprise](https://www.android.com/enterprise/recommended/requirements/). |
| Egenskaper för enhet | Högsta version av operativsystemet | Inte konfigurerat ||
| Systemsäkerhet | Kräv ett lösenord för att låsa upp mobila enheter | Kräver ||
| Systemsäkerhet | Lösenordstyp krävs | Numeriskt avancerat | Organisationer kan behöva uppdatera den här inställningen för att matcha lösenordsprincipen. |
| Systemsäkerhet | Minsta längd på lösenord | 6 | Organisationer kan behöva uppdatera den här inställningen för att matcha lösenordsprincipen. |
| Systemsäkerhet | Max antal minuters inaktivitet innan lösenord krävs| 5 | Organisationer kan behöva uppdatera den här inställningen för att matcha lösenordsprincipen.|
| Systemsäkerhet | Antal dagar tills lösenordet går ut| Inte konfigurerat | Organisationer kan behöva uppdatera den här inställningen för att matcha lösenordsprincipen. |
| Systemsäkerhet | Antal tidigare lösenord för att förhindra återanvändning | Inte konfigurerat | Organisationer kan behöva uppdatera den här inställningen för att matcha lösenordsprincipen. |
| Systemsäkerhet | Kryptering av datalagring på enheten | Kräver ||
| Systemsäkerhet | Blockera appar från okända källor | Blockera ||
| Systemsäkerhet | Körningsintegritet för företagsportalappen | Kräver ||
| Systemsäkerhet | Blockera USB-felsökning på enheten | Blockera | Medan den här inställningen blockerar felsökning med en USB-enhet, inaktiverar den även möjligheten att samla in loggar som kan vara användbara i felsökningssyfte. |
| Systemsäkerhet | Lägsta säkerhetskorrigeringsnivå | Inte konfigurerat | Android-enheter kan ta emot månatliga säkerhetskorrigeringar, men versionen är beroende av OEM-tillverkare och/eller operatörer. Organisationer bör se till att distribuerade Android-enheter tar emot säkerhetsuppdateringar innan de implementerar den här inställningen. De senaste snabbkorrigeringsversionerna finns i [Android Security Bulletins](https://source.android.com/security/bulletin/). |
| Åtgärder för inkompatibilitet | Markera enheten som inkompatibel | Omedelbart | Som standard är principen konfigurerad för att markera enheten som inkompatibel. Det finns ytterligare åtgärder tillgängliga. Mer information finns i [Konfigurera åtgärder för icke-kompatibla enheter i Intune](../protect/actions-for-noncompliance.md).|

### <a name="device-restrictions"></a>Enhetsbegränsningar

| Avsnitt | Inställningen | Värde | Obs! |
| ----- | ----- | ----- | ----- |
| Inställningar för arbetsprofil | Kopiera och klistra in mellan arbetsprofiler och personliga profiler | Blockera ||
| Inställningar för arbetsprofil | Datadelning mellan arbetsprofiler och personliga profiler | Appar i arbetprofilen kan hantera delningsförfrågningar från den personliga profilen ||
| Inställningar för arbetsprofil | Arbetsprofilmeddelanden när enheten är låst | Inte konfigurerat | Om den här inställningen blockeras visas inte känsliga data i arbetsprofilmeddelanden, vilket kan påverka användbarheten. |
| Inställningar för arbetsprofil | Standardappbehörigheter | Standard för enheten | Administratörer behöver granska och justera de behörigheter som beviljats av appar som de distribuerar. |
| Inställningar för arbetsprofil | Lägga till och ta bort konton | Blockera ||
| Inställningar för arbetsprofil | Dela kontakter via Bluetooth | Aktivera | Åtkomst till arbetskontakter är som standard inte tillgängligt på andra enheter, som bilar via Bluetooth-integrering. Om du aktiverar den här inställningen förbättras hands-free upplevelsen för användare. Bluetooth-enheten kan dock cachelagra kontakterna vid första anslutningen. Organisationer bör överväga att balansera användbarhetsscenarier med dataskyddsproblem när den här inställningen implementeras. |
| Inställningar för arbetsprofil | Skärmdump | Blockera ||
| Inställningar för arbetsprofil | Visa arbetskontaktens nummerpresentation i personlig profil | Inte konfigurerat ||
| Inställningar för arbetsprofil | Sök arbetskontakter från en personlig profil | Inte konfigurerat | Om du blockerar användare från att komma åt arbetskontakter från den personliga profilen kan det påverka vissa användbarhetsscenarier, t.ex. textmeddelanden och uppringningsupplevelser i den personliga profilen. Organisationer bör överväga att balansera användbarhetsscenarier med dataskyddsproblem när den här inställningen implementeras. |
| Inställningar för arbetsprofil | Kamera | Inte konfigurerat ||
| Inställningar för arbetsprofil | Tillåt widgetar från arbetsprofilappar | Aktivera ||
| Inställningar för arbetsprofil | Kräv lösenord för arbetsprofil | Kräver ||
| Inställningar för arbetsprofil | Minsta längd på lösenord | 6 | Organisationer kan behöva uppdatera den här inställningen för att matcha lösenordsprincipen. |
| Inställningar för arbetsprofil | Maximalt antal minuter av inaktivitet innan arbetsprofilen låses| 5 | Organisationer kan behöva uppdatera den här inställningen för att matcha lösenordsprincipen. |
| Inställningar för arbetsprofil | Antalet felaktiga inloggningsförsök innan arbetsprofilen rensas| 10 | Organisationer kan behöva uppdatera den här inställningen för att matcha lösenordsprincipen. |
| Inställningar för arbetsprofil | Lösenordets giltighetstid (i dagar) | Inte konfigurerat | Organisationer kan behöva uppdatera den här inställningen för att matcha lösenordsprincipen. |
| Inställningar för arbetsprofil | Lösenordstyp krävs | Numeriskt avancerat ||
| Inställningar för arbetsprofil | Förhindra återanvändning av tidigare lösenord | Inte konfigurerat | Organisationer kan behöva uppdatera den här inställningen för att matcha lösenordsprincipen.|
| Inställningar för arbetsprofil | Upplåsning med fingeravtryck | Inte konfigurerat ||
| Inställningar för arbetsprofil | Smart Lock och andra betrodda agenter | Inte konfigurerat |||
| Enhetslösenord | Minsta längd på lösenord | 6 | Organisationer kan behöva uppdatera den här inställningen för att matcha lösenordsprincipen. |
| Enhetslösenord | Maximalt antal minuter av inaktivitet innan skärmen låses | 5 | Organisationer kan behöva uppdatera den här inställningen för att matcha lösenordsprincipen. |
| Enhetslösenord | Antal felaktiga inloggningar innan enheten rensas | 10 | Den här inställningen utlöser en rensning av arbetsprofilen och inte en rensning av enheten. |
| Enhetslösenord | Lösenordets giltighetstid (i dagar) | Inte konfigurerat | Organisationer kan behöva uppdatera den här inställningen för att matcha lösenordsprincipen. |
| Enhetslösenord | Lösenordstyp krävs | Numeriskt avancerat ||
| Enhetslösenord | Förhindra återanvändning av tidigare lösenord | Inte konfigurerat | Organisationer kan behöva uppdatera den här inställningen för att matcha lösenordsprincipen. |
| Enhetslösenord | Upplåsning med fingeravtryck | Inte konfigurerat ||
| Enhetslösenord | Smart Lock och andra betrodda agenter | Inte konfigurerat ||
| Systemsäkerhet | Hotgenomsökning för appar | Kräver | Den här inställningen säkerställer att Googles Verify Apps-genomsökning aktiveras för slutanvändarenheter. Om det här är konfigurerat blockeras slutanvändaren från åtkomst tills användaren aktiverar Googles appgenomsökning på sin Android-enhet. |
| Systemsäkerhet | Förhindra appinstallationer från okända källor i den privata profilen | Blockera ||

> [!Note]
> När arbetsprofilen för Android Enterprise aktiveras så konfigureras Ett lås som standard för att kombinera lösenord för enheter och arbetsprofil. Ett lås kan inaktiveras för att skilja arbetsprofilen och enhetslösenord vid behov, under inställningar för arbetsprofil.

## <a name="work-profile-high-security"></a>Hög säkerhet för arbetsprofil

Nivå 3 är den rekommenderade konfigurationen för enheter som används av användare eller grupper som har unikt hög risk. Till exempel användare som hanterar mycket känsliga data där obehörigt avslöjande skulle orsaka betydande materiella förluster. Organisationer som kan antas vara föremål för välfinansierade och sofistikerade angrepp bör eftersträva de ytterligare begränsningar som beskrivs nedan. Den här konfigurationen expanderar på konfigurationen på nivå 1 genom att:
- implementera mobilt skydd eller Microsoft Defender ATP.
- begränsa datascenarier för arbetsprofilen.
- implementera starkare lösenordsprinciper.

De principinställningar som tillämpas i nivå 3 innehåller alla principinställningar som rekommenderas för nivå 1. Inställningarna som listas nedan omfattar dock bara de som har lagts till eller ändrats. Dessa inställningar kan ha en något högre inverkan på användare eller program. De tillämpar en säkerhetsnivå som är lämplig för risker riktade mot användare med tillgång till känslig information på mobila enheter.

### <a name="device-compliance"></a>Efterlevnad för enhet

| Avsnitt | Inställningen | Värde | Obs! |
| ----- | ----- | ----- | ----- |
| Microsoft Defender ATP | Kräv att enheten ska hållas vid eller under riskpoängen | Rensa | Den här inställningen kräver Microsoft Defender ATP. Mer information finns i Framtvinga efterlevnad för [Microsoft Defender ATP med villkorsstyrd åtkomst i Intune](../protect/advanced-threat-protection.md).<p>Kunder bör överväga att implementera Microsoft Defender ATP eller en lösning för skydd mot mobilhot. Du behöver inte distribuera båda. |
| Enhetens hälsotillstånd | Kräv att enheten hålls på eller under enhetshotnivån | Skyddad | Den här inställningen kräver en produkt för skydd mot mobilhot. Mer information finns i [Mobile Threat Defense för registrerade enheter](../protect/mtd-device-compliance-policy-create.md).<p>Kunder bör överväga att implementera Microsoft Defender ATP eller en lösning för skydd mot mobilhot. Du behöver inte distribuera båda.|
| Egenskaper för enhet | Lägsta version av operativsystemet | Format: Major.Minor<br>Exempel: 8.0| Microsoft rekommenderar att du konfigurerar den lägsta Android-huvudversionen så att den matchar de Android-versioner som stöds för Microsoft-appar. OEM-tillverkare och enheter som följer rekommenderade krav för Android Enterprise måste ha stöd för den aktuella leveransversionen plus en bokstavsuppgradering. För närvarande rekommenderar Android 8.0 och senare för kunskapsarbetare. De senaste rekommendationerna för Android finns i Rekommenderade krav för Android Enterprise |
| Systemsäkerhet | Antal dagar tills lösenordet går ut | 365 | Organisationer kan behöva uppdatera den här inställningen för att matcha lösenordsprincipen. |
| Systemsäkerhet | Antal tidigare lösenord för att förhindra återanvändning | 5 | Organisationer kan behöva uppdatera den här inställningen för att matcha lösenordsprincipen. |


### <a name="device-restrictions"></a>Enhetsbegränsningar

| Avsnitt | Inställningen | Värde | Obs! |
| ----- | ----- | ----- | ----- |
| Inställningar för arbetsprofil | Arbetsprofilmeddelanden när enheten är låst | Blockera | Om den här inställningen blockeras visas inte känsliga data i arbetsprofilmeddelanden, vilket kan påverka användbarheten. |
| Inställningar för arbetsprofil | Dela kontakter via Bluetooth | Inte konfigurerat | Åtkomst till arbetskontakter är som standard inte tillgängligt på andra enheter, som bilar via Bluetooth-integrering. Om du aktiverar den här inställningen förbättras hands-free upplevelsen för användare. Bluetooth-enheten kan dock cachelagra kontakterna vid första anslutningen. Organisationer bör överväga att balansera användbarhetsscenarier med dataskyddsproblem när den här inställningen implementeras. |
| Inställningar för arbetsprofil | Sök arbetskontakter från en personlig profil | Blockera | Om du blockerar användare från att komma åt arbetskontakter från den personliga profilen kan det påverka vissa användbarhetsscenarier, t.ex. textmeddelanden och uppringningsupplevelser i den personliga profilen. Organisationer bör överväga att balansera användbarhetsscenarier med dataskyddsproblem när den här inställningen implementeras. |
| Inställningar för arbetsprofil | Tillåt widgetar från arbetsprofilappar | Inte konfigurerat ||
| Inställningar för arbetsprofil | Antalet felaktiga inloggningsförsök innan arbetsprofilen rensas | 5 | Organisationer kan behöva uppdatera den här inställningen för att matcha lösenordsprincipen. |
| Inställningar för arbetsprofil | Lösenordets giltighetstid (i dagar) | 365 | Organisationer kan behöva uppdatera den här inställningen för att matcha lösenordsprincipen. |
| Inställningar för arbetsprofil | Förhindra återanvändning av tidigare lösenord | 5 | Organisationer kan behöva uppdatera den här inställningen för att matcha lösenordsprincipen. |
| Inställningar för arbetsprofil | Smart Lock och andra betrodda agenter | Blockera ||
| Enhetslösenord | Antal felaktiga inloggningar innan enheten rensas | 5 | Den här inställningen utlöser en rensning av arbetsprofilen och inte en rensning av enheten. |
| Enhetslösenord | Lösenordets giltighetstid (i dagar) | 365 | Organisationer kan behöva uppdatera den här inställningen för att matcha lösenordsprincipen. |
| Enhetslösenord | Förhindra återanvändning av tidigare lösenord | 5 | Organisationer kan behöva uppdatera den här inställningen för att matcha lösenordsprincipen. |

## <a name="next-steps"></a>Nästa steg

Administratörer kan implementera ovanstående konfigurationsnivåer i sin ringdistributionsmetod för testning och produktionsanvändning genom att importera exemplet [JSON-mallar för säkerhetskonfigurationsramverket för Android Enterprise](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/AndroidEnterprise) med [PowerShell-skript i Intune](https://github.com/microsoftgraph/powershell-intune-samples).
