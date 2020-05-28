---
title: Komma igång med kompatibilitetsinställningar
titleSuffix: Configuration Manager
description: Lär dig mer om grundläggande begrepp och hur kompatibilitetsinställningar fungerar
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: a2742d52-851e-4abc-b623-d12d91684c0b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9143c224082f00b882d3cb557b47b737012393fa
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906342"
---
# <a name="get-started-with-compliance-settings-in-configuration-manager"></a>Kom igång med kompatibilitetsinställningar i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Innan du skapar Configuration Manager kompatibilitetsinställningar måste du först läsa viktiga begrepp och förstå hur de fungerar.  



## <a name="how-compliance-settings-work"></a>Så här fungerar kompatibilitetsinställningar  
Med kompatibilitetsinställningar kan du hantera konfigurationen och efterlevnaden av klienter i din organisation.  

Konfigurationsobjekten kan delas in i två huvudkategorier:  

- **Inställningar för enheter som hanteras med Configuration Manager-klienten** – vanligt vis enheter som du har installerat Configuration Manager klient program vara för att låta dig hantera enheten.  

- **Inställningar för enheter som hanteras utan Configuration Manager klienten** – vanligt vis enheter som hanteras med Microsoft Intune eller med Configuration Manager lokal enhets hantering.  



## <a name="what-devices-are-supported"></a>Vilka enheter stöds?  

| Enhetstyp | Mer information |  
|------------|----------------------|  
| Windows-datorer (med Configuration Manager-klienten) | Skapa anpassade konfigurations objekt för att utvärdera objekt, till exempel register nycklar, filer och Active Directory attribut.<br /><br /> När du använder konfigurations objekts typen Windows 10 väljer du inställningar från en fördefinierad lista. |  
| Windows-datorer (registrerade med lokal MDM) | Välj inställningar från en fördefinierad lista. |  
| Windows Phone enheter (registrerade med lokal MDM) | Välj inställningar från en fördefinierad lista. |  
| Mac-datorer (med Configuration Manager-klienten) | Skapa anpassade konfigurations objekt för att utvärdera objekt som macOS-inställningar och resultat som returneras av ett skript. |  



## <a name="what-is-a-configuration-item"></a>Vad är ett konfigurations objekt?  
Ett konfigurations objekt är en behållare som lagrar detaljerad information. Vilken information du konfigurerar beror på typen av konfigurations objekt. Konfigurations objekt kan innehålla följande information:

- **Information om identifierings metoden** är endast för Windows-konfigurationsobjekt som innehåller program inställningar. Den identifierar om ett program har installerats. Den här identifieringen använder Windows Installer-filen för programmet eller genom att använda ett anpassat skript.  

- **Inställningarna** representerar affärs villkor eller tekniska villkor för att utvärdera kompatibiliteten på klient enheter. Konfigurera en ny inställning eller bläddra till en befintlig inställning på en referens dator.  

- **Efterlevnadsprinciper** anger de villkor som definierar kompatibiliteten för en konfigurations objekts inställning. Innan klienten utvärderar en inställning för kompatibilitet måste den ha minst en efterlevnadsprincip. Vissa inställningar reparerar inkompatibla värden. Skapa nya regler eller bläddra till en befintlig inställning i ett konfigurations objekt och välj regler i den.  

- **Plattformar som stöds** är de enhets plattformar som du definierar för att klienten ska utvärdera efterlevnaden av konfigurations objekt. Om du distribuerar ett konfigurations objekt till en enhet som inte finns i listan plattformar som stöds utvärderas inte kompatibiliteten.  



## <a name="what-is-a-configuration-baseline"></a>Vad är en konfigurationsbaslinje?  
Definiera en konfigurations bas linje som innehåller de konfigurations objekt som ska utvärderas. Inkludera även inställningar och regler som beskriver den önskade nivån av efterlevnad. Importera konfigurations data från Configuration Manager konfigurations paket. Microsoft och andra leverantörer definierar dessa konfigurations paket. Eller skapa nya konfigurations objekt och konfigurations bas linjer.  

När du har definierat en konfigurations bas linje distribuerar du den till användar-och enhets samlingar. Klienten utvärderar sedan bas linje inställningarna för kompatibilitet enligt ett schema. Du kan distribuera mer än en konfigurations bas linje till enheter. Denna granularitet ger bättre kontroll över kompatibiliteten. 

Klientenheter utvärderar sin kompatibilitet mot varje distribuerad konfigurationsbaslinje och rapporterar omedelbart resultatet till platsen med hjälp av tillstånds- och statusmeddelanden. Om en enhet för närvarande är frånkopplad från nätverket, men laddat ned konfigurations bas linjen, utvärderas fortfarande kompatibiliteten för konfigurations objekten. Den skickar kompatibilitetsinformation när den återansluter.  

### <a name="monitoring-configuration-baselines"></a>Övervaka konfigurations bas linjer
- Övervaka resultatet av utvärderingen av kompatibiliteten i Configuration Manager-konsolen, under arbets ytan **övervakning** , i noden **distributioner** . Ett exempel:
  - Vanliga orsaker till inkompatibilitet
  - Fel
  - Antalet påverkade användare och enheter
- Kör rapporter för kompatibilitetsinställningar med ytterligare information. Ett exempel:
  - Vilka enheter som är kompatibla eller icke-kompatibla
  - Vilket element i konfigurations bas linjen som gör att en dator inte är kompatibel
- Visa utvärderings resultat för kompatibilitet från Windows-datorer som kör Configuration Manager-klienten. Öppna kontroll panelen **Configuration Manager** och växla till fliken **konfigurationer** .  



## <a name="user-data-and-profiles-configuration-items"></a>Konfigurationsobjekt för användardata och profiler  
Konfigurations objekt för användar data och profiler innehåller inställningar som styr hur användare på datorer som kör Windows 8 och senare hanterar:  
- Mappomdirigering
- Offline-filer
- Nätverks växlings profiler  

Distribuera dessa konfigurations objekt till användar samlingar. Övervaka deras kompatibilitet från noden **övervakning** i Configuration Manager-konsolen. Till skillnad från andra konfigurations objekt lägger du inte till dem i konfigurations bas linjer innan du distribuerar dem. Distribuera dem direkt genom att klicka på **distribuera** i menyfliksområdet.  

Mer information finns i [skapa konfigurations objekt för användar data och profiler](../deploy-use/create-user-data-and-profiles-configuration-items.md).  



## <a name="remote-connection-profiles"></a>Fjärranslutningsprofiler  
Fjärr anslutnings profiler tillhandahåller en uppsättning verktyg och resurser som hjälper dig att skapa, distribuera och övervaka fjärr anslutnings inställningar. Genom att distribuera de här inställningarna till enheter minimerar du den ansträngning som slutanvändarna kräver för att ansluta sina datorer till företags nätverket.  

Mer information finns i [skapa fjärr anslutnings profiler](../deploy-use/create-remote-connection-profiles.md).  



## <a name="windows-edition-upgrade"></a>Windows-versionsuppgradering
Versions uppgraderings principen uppgraderar automatiskt enheter som kör vissa versioner av Windows 10 till en senare version. Den här principen tillhandahåller en ny produkt nyckel eller licens fil som enheten använder för att uppgradera.

Mer information finns i [uppgradera Windows-enheter med uppgraderings principen för versionen](../deploy-use/upgrade-windows-version.md)



## <a name="microsoft-edge-browser-profiles"></a>Profiler för Microsoft Edge-webbläsare
<!-- 1357310 -->
Från och med version 1802, för kunder som använder [Microsoft Edge](https://www.microsoft.com/itpro/microsoft-edge) -webbläsaren på Windows 10-klienter, skapar du en princip för kompatibilitetsinställningar för att konfigurera flera Microsoft Edge-inställningar. 

Mer information finns i [webb läsar profiler för Microsoft Edge](../deploy-use/browser-profiles.md).

