---
title: Aktivera delning av data
titleSuffix: Configuration Manager
description: En referens guide för att dela diagnostikdata med Desktop Analytics.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: be680198-4cea-4378-a686-d52f382ba483
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 999d8441e8c97f0a4b7ad4a92c8175300dcc4ead
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88696454"
---
# <a name="enable-data-sharing-for-desktop-analytics"></a>Aktivera data delning för Skriv bords analys

För att registrera enheter till Skriv bords analys måste de skicka diagnostikdata till Microsoft. Om din miljö använder en proxyserver använder du den här informationen för att konfigurera proxyn.

## <a name="diagnostic-data-levels"></a>Diagnostiska data nivåer

:::image type="content" source="media/diagnostic-data-levels.png" alt-text="Diagram över diagnostiska data nivåer för Skriv bords analys":::

När du integrerar Configuration Manager med Desktop Analytics använder du även den för att hantera den diagnostiska data nivån på enheter. Använd Configuration Manager för bästa möjliga upplevelse.

> [!IMPORTANT]
> I de flesta fall använder du endast Configuration Manager för att konfigurera de här inställningarna. Använd inte heller de här inställningarna i domänens grup princip objekt. Mer information finns i [konflikt lösning](enroll-devices.md#conflict-resolution).

De grundläggande funktionerna i Skriv bords analys fungerar på den **önskade** [nivån för diagnostikdata](/windows/privacy/configure-windows-diagnostic-data-in-your-organization#diagnostic-data-levels). Om du inte konfigurerar den **valfria nivån (begränsad)** i Configuration Manager får du inte följande funktioner i Desktop Analytics:

- Användning av appar
- [Ytterligare App Insights](compat-assessment.md#additional-insights)
- [Distributions status data](deploy-prod.md#address-deployment-alerts)
- [Hälso övervaknings data](health-status-monitoring.md)

Microsoft rekommenderar att du aktiverar den **valfria (begränsade)** diagnostiska data nivån med Desktop Analytics för att maximera de fördelar du får från den.

> [!TIP]
> Den **valfria inställningen (begränsad)** i Configuration Manager är samma inställning som **begränsa utökade diagnostikdata till minimi kravet för Windows Analytics** -princip som är tillgänglig på enheter som kör windows 10, version 1709 och senare.
>
> Enheter som kör Windows 10, version 1703 och tidigare, Windows 8,1 eller Windows 7 har inte den här inställningen. När du konfigurerar den **valfria inställningen (begränsad)** i Configuration Manager, så återgår enheterna till den nivå som **krävs** .
>
> Enheter som kör Windows 10, version 1709 har denna princip inställning. Men när du konfigurerar den **valfria inställningen (begränsad)** i Configuration Manager, kommer dessa enheter också att återgå till den nivå som **krävs** .
>
> I Configuration Manager version 2002 och tidigare hade inställningarna olika namn:<!-- 7363467 -->
>
> | Version 2006 och senare | Version 2002 och tidigare |
> |---------|---------|
> | Obligatorisk | Basic |
> | Valfritt (begränsat) | Utökad (begränsad) |
> | Ej tillämpligt | Optimerad |
> | Valfritt | Fullständig |
>
> Om du tidigare har konfigurerat några enheter på den **förbättrade** nivån, kommer de att återgå till **valfria (begränsat)** när du uppgraderar till version 2006. De skickar då mindre data till Microsoft. Den här ändringen påverkar inte vad du ser i Skriv bords analys.

Mer information om diagnostikdata som delas med Microsoft med **valfritt (begränsat)** finns i [Windows 10 Enhanced Diagnostic data Events and Fields](/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields).

> [!IMPORTANT]
> Microsoft har ett kraftfullt engagemang för att tillhandahålla de verktyg och resurser som hjälper dig att kontrol lera din integritet. Som ett resultat, medan Desktop Analytics stöder Windows 8,1-enheter samlar Microsoft inte in Windows-diagnostikdata från Windows 8,1-enheter som finns i Europeiska länder (EES och Schweiz).

Mer information finns i [Sekretess för Desktop Analytics](privacy.md).

Följande artiklar är också bra för att bättre förstå Windows-diagnostikdata:

- [Windows 10 och GDPR för IT-besluts fattare](/windows/privacy/gdpr-it-guidance)  

- [Konfigurera Windows-diagnostikdata i din organisation](/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

> [!NOTE]
> Klienter som kon figurer ATS för att skicka **valfria (begränsade)** diagnostikdata skickar ungefär 2 MB data till Microsoft-molnet på den första fullständiga genomsökningen. Den dagliga delta varierar mellan 250-400 KB per dag.
>
> Daglig delta-genomsökning sker kl. 3:00 AM (lokal tid för enhet). Vissa händelser skickas vid den första tillgängliga tiden under dagen. Dessa tider kan inte konfigureras.
>
> Mer information finns i [Konfigurera Windows-diagnostikdata i din organisation](https://aka.ms/enterprisetelemetry).  

## <a name="endpoints"></a>Slutpunkter

Om du vill aktivera data delning konfigurerar du proxyservern så att den tillåter följande Internet slut punkter.

> [!IMPORTANT]
> För sekretess och data integritet kontrollerar Windows om ett Microsoft SSL-certifikat (certifikat fästning) vid kommunikation med slut punkter för diagnostikdata. SSL-avlyssning och inspektion är inte möjlig. Om du vill använda Desktop Analytics utesluter du dessa slut punkter från SSL-inspektion.<!-- BUG 4647542 -->

Från och med version 2002, om Configuration Manager-platsen inte kan ansluta till obligatoriska slut punkter för en moln tjänst, genererar den en kritisk status meddelande-ID 11488. När den inte kan ansluta till tjänsten ändras SMS_SERVICE_CONNECTOR komponent status till kritisk. Visa detaljerad status i noden [komponent status](../core/servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus) i Configuration Manager-konsolen.<!-- 5566763 -->

> [!NOTE]
> Mer information om IP-adressintervall för Microsoft finns i [Microsofts offentliga IP-utrymme](https://www.microsoft.com/download/details.aspx?id=53602). Dessa adresser uppdateras regelbundet. Det finns ingen kornig het för tjänsten. alla IP-adresser i dessa intervall kan användas.

[!INCLUDE [Internet endpoints for Desktop Analytics](../core/plan-design/network/includes/internet-endpoints-desktop-analytics.md)]

## <a name="proxy-server-authentication"></a>Autentisering av proxyserver

Om din organisation använder proxyautentisering för Internet åtkomst kontrollerar du att den inte blockerar diagnostikdata på grund av autentisering. Om proxyn inte tillåter att enheter skickar dessa data visas de inte i Skriv bords analys.

### <a name="bypass-recommended"></a>Kringgå (rekommenderas)

Konfigurera proxyservrarna så att de inte kräver proxyautentisering för trafik till slut punkterna för diagnostikdata. Det här alternativet är den mest omfattande lösningen. Det fungerar för alla versioner av Windows 10.  

### <a name="user-proxy-authentication"></a>Autentisering av användar-proxy

Konfigurera enheter så att de använder den inloggade användarens kontext för proxyautentisering. Den här metoden kräver följande konfigurationer:

- Enheter har den aktuella kvalitets uppdateringen för en version av Windows som stöds

- Konfigurera proxy för användar nivå (WinINET-proxy) i **proxyinställningar** i nätverks & Internet grupp för Windows-inställningar. Du kan också använda den äldre kontroll panelen för Internet alternativ.

- Se till att användarna har proxy-behörighet för att få åtkomst till slut punkterna för diagnostikdata. Det här alternativet kräver att enheterna har konsol användare med proxy-behörigheter, så att du inte kan använda den här metoden med hjälp av omdirigerings enheter.

> [!IMPORTANT]
> Autentiseringsmetoden för användarautentisering är inte kompatibel med användning av Microsoft Defender Avancerat skydd. Det här problemet beror på att den här autentiseringen är beroende av register nyckeln **DisableEnterpriseAuthProxy** `0` , medan Microsoft Defender ATP kräver att den är inställd på `1` . Mer information finns i [Konfigurera inställningar för Machine proxy och Internet anslutning i Microsoft Defender ATP](/windows/security/threat-protection/windows-defender-atp/configure-proxy-internet-windows-defender-advanced-threat-protection).

### <a name="device-proxy-authentication"></a>Enhets-proxy-autentisering

Den här metoden har stöd för följande scenarier:

- Konsol lösta enheter, där ingen användare loggar in eller användare av enheten inte har Internet åtkomst

- Autentiserade proxyservrar som inte använder Windows-integrerad autentisering

- Om du också använder Microsoft Defender Avancerat skydd

Den här metoden är den mest komplexa eftersom den kräver följande konfigurationer:

- Se till att enheterna kan komma åt proxyservern via WinHTTP i lokalt system sammanhang. Använd något av följande alternativ för att konfigurera det här beteendet:

  - Kommando raden `netsh winhttp set proxy`

  - WPAD-protokoll (Web Proxy Auto-Discovery)

  - Transparent proxy

  - Konfigurera en enhets omfattande WinINET-proxy med följande grup princip inställning: **gör proxyinställningar per dator (i stället för per användare)** (ProxySettingsPerUser = `1` )

  - Dirigerad anslutning eller som använder Network Address Translation (NAT)

- Konfigurera proxyservrar så att dator kontona i Active Directory kan komma åt data slut punkterna för diagnostikdata. Den här konfigurationen kräver att proxyservrar har stöd för Windows-integrerad autentisering.