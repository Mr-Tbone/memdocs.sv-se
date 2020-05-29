---
title: Grupprincipinställningar
titleSuffix: Configuration Manager
description: Förstå lokala och grup princip inställningar i Windows som används av Configuration Manager-och skriv bords analys
ms.date: 04/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 004ca404-e6fa-47f0-ae77-e44e18a08b33
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 4536adad3114b944baa6c75ac4e246ecddf4a2d2
ms.sourcegitcommit: 555cb8102715afbe06c4de5fdbc943608f00b52c
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/28/2020
ms.locfileid: "84153462"
---
# <a name="group-policy-settings-for-desktop-analytics"></a>Grup princip inställningar för Skriv bords analys

*Gäller för: Configuration Manager (aktuell gren)*

Den här artikeln beskriver de lokala och grup princip inställningarna i Windows som Configuration Manager och skriv bords analys använder.

När Configuration Manager registrerar enheter i Desktop Analytics, ställer den in Windows-principer för att konfigurera enheten. I de flesta fall använder du endast Configuration Manager för att konfigurera de här inställningarna.

## <a name="windows-settings"></a>Windows-inställningar

Configuration Manager anger Windows-principer i en eller båda av följande register nycklar:

- Grup princip objekt (**GPO**):`HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

- **Lokal** princip inställning:`HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`

| Policy | Sökväg | Gäller för | Värde |
|--------|------|------------|-------|
| **CommercialId** | Lokal | Alla Windows-versioner | För att en enhet ska kunna visas i Skriv bords analys konfigurerar du den med din organisations kommersiella ID. |
| **AllowTelemetry**  | GPO | Windows 10 | Ange `1` för **Basic**, `2` för **förbättrad**eller `3` **fullständig** diagnostikdata. Desktop Analytics kräver minst grundläggande diagnostikdata. Microsoft rekommenderar att du använder den förbättrade nivån (begränsad) med Desktop Analytics. Mer information finns i [Konfigurera Windows-diagnostikdata i din organisation](https://docs.microsoft.com/windows/configuration/configure-windows-diagnostic-data-in-your-organization). |
| **LimitEnhancedDiagnosticDataWindowsAnalytics** | GPO | Windows 10, version 1803 och senare | Den här inställningen gäller endast när AllowTelemetry-inställningen är `2` . Den begränsar de utökade diagnostikdata som skickas till Microsoft till enbart de händelser som krävs av Desktop Analytics. Mer information finns i [data händelser och fält för Windows 10-diagnostikdata som samlas in via principen begränsa förbättrad diagnostikdata](https://docs.microsoft.com/windows/configuration/enhanced-diagnostic-data-windows-analytics-events-and-fields). |
| **AllowDeviceNameInTelemetry** | GPO | Windows 10, version 1803 och senare | Gör det möjligt för enheter att skicka enhets namnet. Enhets namnet skickas inte till Microsoft som standard. Om du inte skickar enhets namnet visas det i Skriv bords analys som "okänt". Mer information finns i [enhets namn](enroll-devices.md#device-name). |
| **CommercialDataOptIn** | Lokal | Windows 8,1 och tidigare | Desktop Analytics kräver värdet `1` . Mer information finns i [Välj kommersiella data i Windows 7](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/ee126127\(v=ws.10\)). |
| **RequestAllAppraiserVersions** | Båda | Windows 8,1 och tidigare | Desktop Analytics kräver ett värde för `1` att data insamling ska fungera korrekt. |
| **DisableEnterpriseAuthProxy** | GPO | Alla Windows-versioner | Om din miljö kräver en autentiserad proxy med Windows-integrerad autentisering för Internet åtkomst, kräver Desktop Analytics ett värde för `0` att data insamling ska fungera korrekt. Mer information finns i [Proxy Server-autentisering](enable-data-sharing.md#proxy-server-authentication). |

> [!IMPORTANT]
> I de flesta fall använder du endast Configuration Manager för att konfigurera de här inställningarna. Använd inte heller de här inställningarna i domänens grup princip objekt. Mer information finns i [konflikt lösning](enroll-devices.md#conflict-resolution).

### <a name="settings-from-upgrade-readiness"></a>Inställningar från Uppgraderingsberedskap

Windows Analytics ställer även in följande principer via Uppgraderingsberedskap-skriptet:

- CommercialId
- AllowDeviceNameInTelemetry
- CommercialDataOptIn
- RequestAllAppraiserVersions

Om du körde Uppgraderingsberedskap onboarding-skriptet på en enhet kan de här princip inställningarna fortfarande finnas. Använd inte det äldre skriptet. Innan du registrerar enheten på Desktop Analytics tar du bort dessa tidigare princip inställningar.

## <a name="group-policy-settings"></a>Grupprincipinställningar

I allmänhet använder du Configuration Manager samlingar för att ange inställningar för Skriv bords analys och registrering. Använd direkt medlemskap eller frågor för att ta med eller undanta enheter från samlingen. Mer information finns i [så här skapar du samlingar](../core/clients/manage/collections/create-collections.md).

Configuration Manager konfigurerar inställningar för affärs-ID och diagnostikdata i mål samlingen. Om du behöver konfigurera olika inställningar för diagnostikdata för olika grupper av enheter använder du grup princip inställningar för att åsidosätta Configuration Manager inställningar. Du måste till exempel ange **förbättrad (begränsad)** nivå för vissa enheter och **Basic** för andra. Vissa enheter kan ha olika [autentiseringsinställningar för proxyservern](enable-data-sharing.md#proxy-server-authentication) .

Relevanta grup princip inställningar finns på följande sökväg: **dator konfiguration**  >  **administrativa mallar**  >  **Windows-komponenter**  >  **data insamling och för hands versioner**.

Grup princip inställningar ändrar bara register inställningar i följande nyckel:`HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

> [!IMPORTANT]
> När du använder grup princip inställningar för att aktivera komplexa scenarier bör du särskilt uppmärksamma princip inställningar som kan orsaka konfigurations konflikter. Configuration Manager konfigurerar bara [Windows-inställningar](#windows-settings) *om värdet inte redan finns*. Grup princip inställningar har företräde framför Configuration Manager inställningar, så vissa grup princip konfigurationer kan orsaka problem med Desktop Analytics.

### <a name="group-policy-settings-that-could-conflict-with-configuration-manager-settings-for-desktop-analytics"></a>Grup princip inställningar som kan vara i konflikt med Configuration Manager inställningar för Skriv bords analys

Grup princip inställningarna i följande tabell har störst potential för att orsaka en konflikt med Windows-inställningarna som Configuration Manager uppsättningar på enheter som den registrerar till Skriv bords analys:

| Visningsnamn | Registervärde | Påverkan på enheter som har registrerats i Skriv bords analys |
|--------------|----------------|-------------------------------------------------|
| **Konfigurera det kommersiella ID: t** | CommercialId | Om du anger ett annat värde för den här principen åsidosätts det kommersiella ID som anges av Configuration Manager. Om det inte är samma ID kan konfigurerade enheter inte visas i Skriv bords analys. |
| **Tillåt telemetri** | AllowTelemetry | Om du anger ett annat värde för den här principen åsidosätts den globala diagnostikdata som du angav i Configuration Manager för mål samlingen. |
| **Begränsa utökade diagnostikdata till minimi kravet för Windows Analytics** | LimitEnhancedDiagnosticDataWindowsAnalytics | Den här principen är beroende av den tidigare AllowTelemetry-inställningen. Beroende på vilken nivå du angav i Configuration Manager eller med grup princip, kan den här principen ändra nivån för diagnostikdata på enheten till **förbättrad** eller **utökad (begränsad)**. Den här principen gäller endast om AllowTelemetry har värdet `2` (**utökad**). |
| **Tillåt att enhets namn skickas i Windows-diagnostikdata** | AllowDeviceNameInTelemetry | Om du väljer att skicka enhets namn i Configuration Manager kan du åsidosätta det genom att konfigurera principen till inaktive rad. När du inaktiverar den här inställningen visas enhets namn som "okända" i Skriv bords analys. Mer information finns i [enhets namn](enroll-devices.md#device-name). |
| **Konfigurera användning av autentiserad proxy för tjänsten för anslutna användar upplevelser och telemetri** | DisableEnterpriseAuthProxy | Om du konfigurerar Configuration Manager enheter att använda autentiserad proxy ( `0` ) och sedan konfigurerar den här principen för att **inaktivera användning av autentiserad proxy** ( `1` ), skickar enheten diagnostikdata i system kontexten i stället för användarens kontext. Om du inte konfigurerar enheten med en proxyserver i system kontext, eller om enheten inte kan autentisera till proxyn, kan Windows inte skicka diagnostikdata till Desktop Analytics. |

> [!NOTE]
> Den äldre principen **Konfigurera anslutna användar upplevelser och telemetri** (TelemetryProxy) gör det möjligt för Windows att vidarebefordra diagnostikdata till en dedikerad proxy, i stället för att använda proxyn för användare (wininet) eller enhet (WinHTTP). Vissa Windows-komponenter stöder inte den här principen. Om du använder den här principen kan det orsaka problem med data kvaliteten i Desktop Analytics.

#### <a name="behavior-of-disabled-settings"></a>Beteende för inaktiverade inställningar

Om du konfigurerar dessa grup princip inställningar till **inaktive rad**har den olika effekter på system beteendet.

- När du inaktiverar **CommercialId** -principen tar Windows bort registervärdet. Configuration Manager inställningen för det kommersiella ID: t som anges i register Sök vägen för den lokala principen gäller för enheten.

- För principer som Configuration Manager anger i samma register plats som grup princip, tas registervärdet bort när du inaktiverar inställningen i grup princip. Configuration Manager kommer att ställa in det igen på nästa princip bearbetnings cykel och sedan tas den bort i nästa grup princip uppdatering. Den här konstanta ändringen i konfigurationen kan orsaka oönskade beteenden med Desktop Analytics.

  - Om du anger att dessa grup princip inställningar **inte ska konfigureras**, tar Windows bort värdet en gång, men fortsätter inte att ta bort den. Med den här konfigurationen kan Configuration Manager tillämpa värdena som förväntat.

### <a name="group-policy-settings-to-customize-the-user-experience"></a>Grup princip inställningar för att anpassa användar upplevelsen

Dessa grup princip inställningar krävs inte av Configuration Manager eller Skriv bords analys. Du kan konfigurera dem i grup principer för att konfigurera användarnas upplevelse med Windows-diagnostikdata.

| Visningsnamn | Registervärde | Påverkan på enheter som har registrerats i Skriv bords analys |
|--------------|----------------|-------------------------------------------------|
| **Konfigurera anmälan om ändring av telemetri** | DisableTelemetryOptInChangeNotification | Från och med Windows 10, version 1803 meddelar Windows användare när nivån för diagnostikdata ändras. Använd den här principen för att inaktivera meddelanden. |
| **Konfigurera alternativet för att välja användar gränssnitt för telemetri** | DisableTelemetryOptInSettingsUx | När du konfigurerar den diagnostiska data nivån ställer du in den övre gräns värdet för enheten. Från och med Windows 10, version 1803, kan användarna ange en lägre nivå. Använd den här principen för att hindra användare från att ändra diagnostisk nivå. Mer information finns i [Konfigurera Windows-diagnostikdata i din organisation](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management). |
| **Inaktivera borttagning av diagnostikdata** | DisableDeviceDelete | Från och med Windows 10, version 1809, kan användare ta bort diagnostikdata från sidan med inställningar för **feedback & feedback** . Använd den här principen för att förhindra borttagning av diagnostikdata som Microsoft samlar in från enheten. |
| **Inaktivera visning av diagnostikdata** | DisableDiagnosticDataViewer | Från och med Windows 10, version 1809, kan användare aktivera och öppna visnings programmet för diagnostikdata från sidan Inställningar för **feedback för diagnostik &** . Använd den här principen för att inaktivera visnings programmet för diagnostikdata i Windows-inställningar och förhindra att det visar diagnostikdata som Microsoft samlar in från enheten.|
