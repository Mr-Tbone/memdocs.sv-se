---
title: Övervaka Cloud Management Gateway
titleSuffix: Configuration Manager
description: Övervaka klienter och nätverks trafik via Cloud Management Gateway (CMG).
ms.date: 06/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 15f72f80-9850-40ce-9c3a-443ba04b6a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b3233dc2f6bd13e56f7555536c95d42a34e01d5e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714229"
---
# <a name="monitor-cloud-management-gateway"></a>Övervaka Cloud Management Gateway

*Gäller för: Configuration Manager (aktuell gren)*

När CMG (Cloud Management Gateway) körs och klienterna ansluter via den kan du övervaka klienter och nätverks trafik för att kontrol lera att du vet hur tjänsten fungerar.


## <a name="monitor-clients"></a>Övervaka klienter

Klienter som är anslutna via CMG visas i Configuration Manager-konsolen på samma sätt som lokala klienter gör. Mer information finns i [övervaka klienter](../monitor-clients.md).


## <a name="monitor-traffic-in-the-console"></a>Övervaka trafik i-konsolen

Övervaka trafik på CMG med hjälp av Configuration Manager-konsolen:

1. Gå till arbets ytan **Administration** , expandera **Cloud Services**och välj noden **Cloud Management Gateway** .  

2. Välj CMG i list rutan.  

3. Visa trafik informationen i informations fönstret för CMG anslutnings punkt och de plats system roller som den ansluter till. Dessa statistik visar vilka klient begär Anden som kommer till dessa roller. Förfrågningarna omfattar princip, plats, registrering, innehåll, inventering och klient meddelanden.<!-- SCCMDocs#1208 -->

## <a name="set-up-outbound-traffic-alerts"></a>Konfigurera utgående trafik varningar

Varningar om utgående trafik hjälper dig att känna till när nätverks trafiken närmar sig en tröskel nivå på 14 dagar. När du skapar CMG kan du konfigurera trafik aviseringar. Om du har hoppat över den delen kan du fortfarande konfigurera aviseringarna när tjänsten har körts. Justera aviserings inställningarna när som helst.

1. Gå till arbets ytan **Administration** , expandera **Cloud Services**och välj noden **Cloud Management Gateway** .  

2. Välj CMG i list rutan och välj sedan **Egenskaper** i menyfliksområdet.  

3. Gå till fliken **aviseringar** om du vill aktivera tröskelvärde och aviseringar. Ange 14 dagars data tröskel i gigabyte (GB). Ange också tröskelvärdet i procent för att höja de olika varnings nivåerna.  

4. När du är klar väljer du **Ok**.  


## <a name="monitor-logs"></a>Övervaka loggar

CMG genererar poster i ett antal loggfiler. Mer information finns i [Configuration Manager loggar](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway).


## <a name="cloud-management-dashboard"></a>Instrument panel för moln hantering

<!--1358461-->
Från och med version 1806 tillhandahåller moln hanterings instrument panelen en centraliserad vy för CMG-användning. När platsen har publicerats till [Azure-tjänster](../../../servers/deploy/configure/azure-services-wizard.md) för moln hantering visas även data om moln användare och enheter.  

Följande skärm bild är en del av instrument panelen för moln hantering som visar två av de tillgängliga panelerna:  
![Instrument panels paneler för moln hantering CMG trafik och aktuella online-klienter](media/1358461-cmg-dashboard.png)

Gå till arbets ytan **övervakning** i Configuration Manager-konsolen. Välj noden **moln hantering** och Visa paneler på instrument panelen.  


## <a name="connection-analyzer"></a>Anslutnings analys

Från och med version 1806 använder du CMG Connection Analyzer för att kontrol lera i real tid för att under lätta fel sökningen. I konsol verktyget kontrol leras tjänstens aktuella status och kommunikations kanalen genom CMG anslutnings punkt till alla hanterings platser som tillåter CMG-trafik.

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen. Expandera **Cloud Services** och välj noden **Cloud Management Gateway** .  

2. Välj mål CMG-instansen och välj sedan **anslutnings analys** i menyfliksområdet.  

3. I fönstret CMG Connection Analyzer väljer du något av följande alternativ för att autentisera med tjänsten:  

     1. **Azure AD-användare**: Använd det här alternativet om du vill simulera kommunikation på samma sätt som en molnbaserad användar identitet som är inloggad på en Azure AD-ansluten Windows 10-enhet. Klicka på **Logga** in för att ange autentiseringsuppgifterna på ett säkert sätt för det här Azure AD-användarkontot.  

     2. **Klient certifikat**: Använd det här alternativet om du vill simulera kommunikation på samma sätt som en Configuration Manager-klient med ett [certifikat för klientautentisering](certificates-for-cloud-management-gateway.md#bkmk_clientauth).  

4. Välj **Starta** för att starta analysen. Resultatet visas i analys fönstret. Välj en post om du vill visa mer information i fältet Beskrivning.  


## <a name="stop-cmg-when-it-exceeds-threshold"></a><a name="bkmk_stop"></a>Stoppa CMG när den överskrider tröskelvärdet

<!--3735092-->
Från och med version 1902 kan Configuration Manager nu stoppa en CMG-tjänst när den totala data överföringen går över gränsen. Använd [aviseringar](#set-up-outbound-traffic-alerts) för att utlösa meddelanden när användningen når varnings-eller kritiska nivåer. För att minska eventuella oväntade Azure-kostnader på grund av en ökning i användningen stänger moln tjänsten av den här funktionen.

> [!Important]  
> Även om tjänsten inte körs finns det fortfarande kostnader som är kopplade till moln tjänsten. Om du stoppar tjänsten elimineras inte alla associerade Azure-kostnader. Ta bort [CMG](setup-cloud-management-gateway.md#modify-a-cmg)om du vill ta bort all kostnad för moln tjänsten.  
>
> När CMG-tjänsten stoppas kan inte Internetbaserade klienter kommunicera med Configuration Manager.  

Den totala data överföringen (utgående) inkluderar data från moln tjänsten och lagrings kontot. Dessa data kommer från följande flöden:

- CMG till klient  
- CMG till plats, inklusive CMG-loggfiler  
- Om du aktiverar CMG för innehåll, lagrings konto till klient  

Mer information om dessa data flöden finns i [CMG-portar och data flöde](plan-cloud-management-gateway.md#ports-and-data-flow).

Tröskelvärdet för lagrings aviseringen är separat. Den aviseringen övervakar kapaciteten för din Azure Storage-instans.

När du väljer CMG-instansen i **Cloud Management Gateway** -noden i-konsolen kan du se den totala data överföringen i informations fönstret.

Configuration Manager kontrollerar tröskelvärdet var sjätte minut. Om det finns en plötslig insamling i användningen kan Configuration Manager ta upp till sex minuter innan tröskelvärdet överskrids och tjänsten stoppas.

### <a name="process-to-stop-the-cloud-service-when-it-exceeds-threshold"></a>Processen att stoppa moln tjänsten när den överskrider tröskelvärdet

1. [Konfigurera utgående trafik varningar](#set-up-outbound-traffic-alerts).  

2. På fliken **aviseringar** i fönstret Egenskaper för CMG aktiverar du alternativet att **stoppa tjänsten när det kritiska tröskelvärdet överskrids**.  

För att testa den här funktionen kan du tillfälligt minska ett av följande värden:  

- **14-dagars tröskel för utgående data överföring (GB)**. Standardvärdet är `10000`.  

- **Procent andel av tröskelvärdet för att höja den kritiska aviseringen**. Standardvärdet är `90`.  
