---
title: Säkerhetskonfigurationer för fullständigt hanterade Android Enterprise
titleSuffix: Microsoft Intune
description: Läs om de föreslagna inställningarna för fullständigt hanterad Android Enterprise grundläggande, utökad och hög säkerhet.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/24/2020
ms.topic: reference
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
ms.openlocfilehash: 01c8c0ffba349966c99e1cbd90dbdfc10a5c9782
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/18/2020
ms.locfileid: "86461172"
---
# <a name="android-enterprise-fully-managed-security-configurations"></a>Säkerhetskonfigurationer för fullständigt hanterade Android Enterprise

Som en del av [Säkerhetskonfigurationsramverket för Android Enterprise](android-configuration-framework.md), tillämpa följande inställningar för användare av fullständigt hanterad Android Enterprise. Mer information om varje principinställning finns i [Android Enterprise-inställningar för enhetsägare för att markera enheter som kompatibla eller inte kompatibla med Intune](../protect/compliance-policy-create-android-for-work.md#fully-managed-dedicated-and-corporate-owned-work-profile) och [Android Enterprise-enhetsinställningar för att tillåta eller begränsa funktioner med Intune](../configuration/device-restrictions-android-for-work.md#fully-managed-dedicated-and-corporate-owned-work-profile).

När du väljer inställningarna måste du granska och kategorisera användningsscenarier. Konfigurera sedan användare enligt riktlinjerna för den valda säkerhetsnivån. Du kan justera de föreslagna inställningarna utifrån organisationens behov. Se till att ditt säkerhetsteam utvärderar hotmiljön, riskbenägenhet och inverkan på användbarhet.

För företagsägda, fullständigt hanterade enheter, finns det tre rekommenderade ramverk för säkerhetskonfiguration:

- [Fullständigt hanterad grundläggande säkerhet (nivå 1)](#fully-managed-basic-security) 
- [Fullständigt hanterad utökad säkerhet (nivå 2)](#fully-managed-enhanced-security)
- [Fullständigt hanterad hög säkerhet (nivå 3)](#fully-managed-high-security) 

## <a name="fully-managed-basic-security"></a>Fullständigt hanterad grundläggande säkerhet

Nivå 1 är den rekommenderade minsta säkerhetskonfigurationen för mobila enheter som ägs av organisationen.

Principerna i nivå 1 framtvingar en rimlig dataåtkomstnivå och minimerar påverkan på användare. Detta görs genom att framtvinga lösenordsprinciper, en minsta operativsystemsversion, SafetyNet-enhetsattestering och inaktivera vissa enhetsfunktioner (t.ex. USB-filöverföringar). 

### <a name="device-compliance"></a>Efterlevnad för enhet

| Avsnitt | Inställningen | Värde | Obs! |
| ----- | ----- | ----- | ----- |
| Microsoft Defender ATP | Kräv att enheten ska hållas vid eller under riskpoängen | Inte konfigurerat ||
| Enhetens hälsotillstånd | Kräv att enheten hålls på eller under enhetshotnivån | Inte konfigurerat||
| Enhetens hälsotillstånd | SafetyNet-enhetsattestering | Kontrollera grundläggande integritet och certifierade enheter | Den här inställningen konfigurerar Googles SafetyNet-attestering för slutanvändarenheter. Grundläggande integritet kontrollerar enhetens integritet. Rotade enheter, emulatorer, virtuella enheter och enheter med tecken på manipulation misslyckas med grundläggande integritet.<br>Grundläggande integritet och certifierade enheter validerar enhetens kompatibilitet med Googles tjänster. Endast oförändrade enheter som har certifierats av Google kan godkännas av den här kontrollen. |
| Egenskaper för enhet | Lägsta version av operativsystemet | Format: Major.Minor<br>Exempel: 8.0| Microsoft rekommenderar att du konfigurerar den lägsta Android-huvudversionen så att den matchar de Android-versioner som stöds för Microsoft-appar. OEM-tillverkare och enheter som följer rekommenderade krav för Android Enterprise måste ha stöd för den aktuella leveransversionen plus en bokstavsuppgradering. För närvarande rekommenderar Android 8.0 och senare för kunskapsarbetare. De senaste rekommendationerna för Android finns i [Rekommenderade krav för Android Enterprise](https://www.android.com/enterprise/recommended/requirements/). |
| Egenskaper för enhet | Högsta version av operativsystemet | Inte konfigurerat ||
| Egenskaper för enhet | Lägsta säkerhetskorrigeringsnivå | Inte konfigurerat | Android-enheter kan ta emot månatliga säkerhetskorrigeringar, men versionen är beroende av OEM-tillverkare och/eller operatörer. Organisationer bör se till att distribuerade Android-enheter tar emot säkerhetsuppdateringar innan de implementerar den här inställningen. De senaste snabbkorrigeringsversionerna finns i [Android Security Bulletins](https://source.android.com/security/bulletin/). |
| Systemsäkerhet | Kräv ett lösenord för att låsa upp mobila enheter | Kräver ||
| Systemsäkerhet | Lösenordstyp krävs | Numeriskt avancerat | Organisationer kan behöva uppdatera den här inställningen för att matcha lösenordsprincipen. |
| Systemsäkerhet | Minsta längd på lösenord | 6 | Organisationer kan behöva uppdatera den här inställningen för att matcha lösenordsprincipen. |
| Systemsäkerhet | Max antal minuters inaktivitet innan lösenord krävs| 5 | Organisationer kan behöva uppdatera den här inställningen för att matcha lösenordsprincipen.|
| Systemsäkerhet | Antal dagar tills lösenordet går ut| Inte konfigurerat ||
| Systemsäkerhet |    Antal lösenord som krävs innan användaren kan återanvända ett lösenord | Inte konfigurerat ||
| Systemsäkerhet | Kryptering av datalagring på enheten | Kräver ||
| Åtgärder för inkompatibilitet | Markera enheten som inkompatibel | Omedelbart | Som standard är principen konfigurerad för att markera enheten som inkompatibel. Det finns ytterligare åtgärder tillgängliga. Mer information finns i [Konfigurera åtgärder för icke-kompatibla enheter i Intune](../protect/actions-for-noncompliance.md).|

### <a name="device-restrictions"></a>Enhetsbegränsningar

| Avsnitt | Inställningen | Värde | Obs! |
| ----- | ----- | ----- | ----- |
| Allmänt | Skärmdump | Inte konfigurerat ||
| Allmänt | Kamera | Inte konfigurerat ||
| Allmänt | Standard behörighetsprincip | Standard för enheten ||
| Allmänt | Datum- och tidsändringar | Inte konfigurerat ||
| Allmänt | Volymändringar | Inte konfigurerat ||
| Allmänt | Fabriksåterställning | Blockera ||
| Allmänt | Säker start | Blockera ||
| Allmänt | Statusfält | Inte konfigurerat ||
| Allmänt | Dataroamingtjänster | Inte konfigurerat ||
| Allmänt | Ändringar i Wi-Fi-inställning | Inte konfigurerat ||
| Allmänt | Bluetooth-konfiguration | Inte konfigurerat ||
| Allmänt | Internetdelning och åtkomst till surfpunkter | Inte konfigurerat ||
| Allmänt | USB-lagring | Inte konfigurerat ||
| Allmänt | USB-filöverföring | Blockera ||
| Allmänt | Externa medier | Blockera ||
| Allmänt | Överför data via NFC | Inte konfigurerat ||
| Allmänt | Felsökningsfunktioner | Inte konfigurerat ||
| Allmänt | Mikrofonjustering | Inte konfigurerat ||
| Allmänt | E-post för skydd mot fabriksåterställning | Inte konfigurerat ||
| Allmänt | Nätverkshjälp | Inte konfigurerat ||
| Allmänt | Systemuppdatering | Automatiskt ||
| Allmänt | Meddelandefönster | Inte konfigurerat ||
| Allmänt | Hoppa över tips vid första användning | Inte konfigurerat ||
| Systemsäkerhet | Hotgenomsökning för appar |Kräver ||
| Enhetsmiljö | Registreringsprofiltyp | Fullständigt hanterad ||
| Enhetsmiljö | Gör Microsoft Launcher till standardstartprogram | Inte konfigurerat | Organisationer kan välja att implementera Microsoft Launcher för att säkerställa en konsekvent startskärmsupplevelse på fullständigt hanterade enheter. Mer information finns i [Så här konfigurerar du Microsoft Launcher på fullständigt hanterade Android Enterprise-enheter med Intune](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-setup-microsoft-launcher-on-android-enterprise-fully/ba-p/1482134) |
| lösenordsinställning | Inaktivera låsskärm | Inte konfigurerat ||
| lösenordsinställning | Inaktiverade låsskärmsfunktioner | 0 valda ||
| lösenordsinställning | Lösenordstyp krävs | Numeriskt avancerat ||
| lösenordsinställning | Minsta längd på lösenord | 6 ||
| lösenordsinställning | Antal dagar tills lösenordet går ut | Inte konfigurerat ||
| lösenordsinställning | Antal lösenord som krävs innan användaren kan återanvända ett lösenord | Inte konfigurerat ||
| lösenordsinställning | Antal felaktiga inloggningar innan enheten rensas | 10 ||
| Energiinställningar | Tid innan skärmen låses | 5 ||
| Energiinställningar | Skärmen är igång när enheten är ansluten | Inte konfigurerat ||
| Användare och konton | Lägg till nya användare | Inte konfigurerat ||
| Användare och konton | Borttagning av användare | Inte konfigurerat ||
| Användare och konton | Kontoändringar (endast dedikerade enheter) | Inte konfigurerat ||
| Användare och konton | Personliga Google-konton | Inte konfigurerat ||
| Användare och konton | Användaren kan konfigurera autentiseringsuppgifter | Blockera ||
| Program | Tillåt installation från okända källor | Inte konfigurerat ||
| Program | Tillåt åtkomst till alla appar i Google Play-butiken | Inte konfigurerat | Som standard kan användarna inte installera personliga appar från Google Play Store på fullständigt hanterade enheter. Om organisationen vill tillåta att fullständigt hanterade enheter används för personligt bruk bör du överväga att ändra den här inställningen. |
| Program | Automatiska appuppdateringar | Endast Wi-Fi | Organisationer bör justera den här inställningen om det behövs eftersom det kan hända att dataabonnemangsavgifter kan uppstå om appuppdateringar uppstår över det mobila nätverket. |

## <a name="fully-managed-enhanced-security"></a>Fullständigt hanterad utökad säkerhet

Nivå 2 är den rekommenderade dataskyddskonfigurationen som standard för företagsägda enheter där användare får åtkomst till mer känslig information. De här enheterna är ett naturligt mål för angripare i dagens företagsvärld. De här inställningarna förutsätter inte en stor personal med högt utbildad säkerhetspersonal. De bör därför vara tillgängliga för de flesta företagsorganisationer. Den här konfigurationen expanderar vid konfigurationen på nivå 1 genom att använda starkare lösenordsprinciper och inaktivera användar-/kontofunktioner.

Nivå 2-inställningarna innehåller alla principinställningar som rekommenderas för nivå 1. Inställningarna som listas nedan omfattar bara de som har lagts till eller ändrats. Dessa inställningar kan ha en något högre inverkan på användare eller program. De tillämpar en säkerhetsnivå som är lämplig för risker riktade mot användare med tillgång till känslig information på mobila enheter.

### <a name="device-compliance"></a>Efterlevnad för enhet

| Avsnitt | Inställningen | Värde | Obs! |
| ----- | ----- | ----- | ----- |
| Systemsäkerhet | Antal dagar tills lösenordet går ut | 365 | Organisationer kan behöva uppdatera den här inställningen för att matcha lösenordsprincipen. |
| Systemsäkerhet |    Antal lösenord som krävs innan användaren kan återanvända ett lösenord | 5 | Organisationer kan behöva uppdatera den här inställningen för att matcha lösenordsprincipen. |

### <a name="device-restrictions"></a>Enhetsbegränsningar

| Avsnitt | Inställningen | Värde | Obs! |
| ----- | ----- | ----- | ----- |
| Allmänt | E-post för skydd mot fabriksåterställning | E-postadresser för Google-konto ||
| Allmänt | Lista över e-postadresser (endast alternativet för Google-kontoadresser) | example@gmail.com | Uppdatera den här principen manuellt för att ange Google-adresserna för enhetsadministratörer som kan låsa upp enheterna när de har rensats. |
| Enhetslösenord | Antal dagar tills lösenordet går ut | 365 | Organisationer kan behöva uppdatera den här inställningen för att matcha lösenordsprincipen. |
| Enhetslösenord | Antal lösenord som krävs innan användaren kan återanvända ett lösenord | 5 | Organisationer kan behöva uppdatera den här inställningen för att matcha lösenordsprincipen. |
| Enhetslösenord | Antal felaktiga inloggningar innan enheten rensas | 5 ||
| Användare och konton | Lägg till nya användare | Blockera ||
| Användare och konton | Borttagning av användare | Blockera ||
| Användare och konton | Personliga Google-konton | Blockera ||

## <a name="fully-managed-high-security"></a>Fullständigt hanterad hög säkerhet

Nivå 3 är den rekommenderade konfigurationen för båda:
- organisationer med stora och avancerade säkerhetsorganisationer.
- specifika användare och grupper som kommer att vara särskilda måltavlor för angripare.
Sådana organisationer är vanligtvis måltavlor för välfinansierade och sofistikerade angripare. De förtjänar därmed de ytterligare begränsningar och kontroller som anges nedan.

Den här konfigurationen expanderar på nivå 2 genom att:
- öka lägsta operativsystemversion.
- se till att enheten är kompatibel genom att framtvinga den säkraste nivån för Microsoft Defender ATP eller Skydd mot mobilhot.
- öka lägsta operativsystemversion.
- framtvinga ytterligare enhetsbegränsningar (t.ex. inaktivera oredigerade meddelanden på låsskärmen).
- kräv att appar alltid ska vara uppdaterade. 

De principinställningar som tillämpas i nivå 3 innehåller alla principinställningar som rekommenderas för nivå 2. Inställningarna som listas nedan omfattar dock bara de som har lagts till eller ändrats. Dessa inställningar kan ha en betydande inverkan på användare eller program. De framtvingar en säkerhetsnivå som är lämplig för risker riktade mot organisationer.


### <a name="device-compliance"></a>Efterlevnad för enhet

| Avsnitt | Inställningen | Värde | Obs! |
| ----- | ----- | ----- | ----- |
| Microsoft Defender ATP | Kräv att enheten ska hållas vid eller under riskpoängen | Rensa | Den här inställningen kräver Microsoft Defender ATP. Mer information finns i Framtvinga efterlevnad för [Microsoft Defender ATP med villkorsstyrd åtkomst i Intune](../protect/advanced-threat-protection.md).<p> Kunder bör överväga att implementera Microsoft Defender ATP eller en lösning för skydd mot mobilhot. Du behöver inte distribuera båda. |
| Enhetens hälsotillstånd | Kräv att enheten hålls på eller under enhetshotnivån | Skyddad | Den här inställningen kräver en produkt för skydd mot mobilhot. Mer information finns i [Mobile Threat Defense för registrerade enheter](../protect/mtd-device-compliance-policy-create.md).<p>Kunder bör överväga att implementera Microsoft Defender ATP eller en lösning för skydd mot mobilhot. Du behöver inte distribuera båda.|
| Egenskaper för enhet | Lägsta version av operativsystemet | Format: Major.Minor<br>Exempel: 10.0| Microsoft rekommenderar att du konfigurerar den lägsta Android-huvudversionen så att den matchar de Android-versioner som stöds för Microsoft-appar. OEM-tillverkare och enheter som följer rekommenderade krav för Android Enterprise måste ha stöd för den aktuella leveransversionen plus en bokstavsuppgradering. För närvarande rekommenderar Android 8.0 och senare för kunskapsarbetare. De senaste rekommendationerna för Android finns i Rekommenderade krav för Android Enterprise |

### <a name="device-restrictions"></a>Enhetsbegränsningar

| Avsnitt | Inställningen | Värde | Obs! |
| ----- | ----- | ----- | ----- |
| Allmänt | Datum- och tidsändringar | Blockera ||
| Allmänt | Internetdelning och åtkomst till surfpunkter | Blockera ||
| Allmänt | Överför data via NFC | Blockera ||
| Enhetslösenord | Inaktiverade låsskärmsfunktioner | Betrodda agenter, oredigerade meddelanden ||
| Program | Automatiska appuppdateringar | Alltid | Organisationer bör justera den här inställningen om det behövs eftersom det kan hända att dataabonnemangsavgifter kan uppstå om appuppdateringar uppstår över det mobila nätverket. |


## <a name="next-steps"></a>Nästa steg

Administratörer kan implementera ovanstående konfigurationsnivåer i sin ringdistributionsmetod för testning och produktionsanvändning genom att importera exemplet [JSON-mallar för säkerhetskonfigurationsramverket för Android Enterprise](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/AndroidEnterprise) med [PowerShell-skript i Intune](https://github.com/microsoftgraph/powershell-intune-samples).
