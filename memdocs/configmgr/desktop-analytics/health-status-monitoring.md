---
title: Övervakning av hälsotillstånd
titleSuffix: Configuration Manager
description: Lär dig mer om hur hälso tillstånds övervakning fungerar i Desktop Analytics.
ms.date: 01/16/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 343dbe2a-597c-4719-b7ac-45b1f39b49ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: b4663ca5640bcfea4338912ff471a3253b744d5f
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125839"
---
# <a name="health-status-monitoring-in-desktop-analytics"></a>Övervakning av hälso status i Skriv bords analys

När du [distribuerar en uppdatering av produktionen](deploy-prod.md)använder du Skriv bords analys för att övervaka enhetens hälso tillstånd. Den här artikeln beskriver i detalj hur hälso övervakning fungerar.

Mer information om hur du använder den här funktionen finns i [övervaka hälsan för uppdaterade enheter](deploy-prod.md#bkmk_monitor).

![Skärm bild av sidan övervaka hälso tillstånd i Skriv bords analys](media/monitor-health.png)

> [!NOTE]  
> Skriv bords analys samlar endast in hälso data från enheter som tillhandahåller användnings data som den kan använda som en nämnare. Det innebär att den inte innehåller enheter som kör Windows 7 och Windows 10 och som inte är inställda på att dela diagnostikdata på nivån valfri (begränsad). Om mer än 10% av enheter som kör Windows 10 är inställda på att dela diagnostikdata på andra nivåer än valfria (begränsat) visas en varning i informations området på sidan **övervaka hälsa** .  

Om du vill visa mer information om en speciell app markerar du den i listan.

## <a name="apps"></a>Appar

### <a name="health-status-factors"></a>Hälso status faktorer

![Hälso status faktorer för en app i Desktop Analytics](media/monitor-health-status-factors.png)

Skriv bords analys övervakar följande hälso status faktorer för appar:

- **% Enheter med krascher**: under de senaste två veckorna har antalet enheter där den här appen har kraschat dividerat med antalet enheter där appen har använts. I den här vyn kan du se om appens stabilitet har ökat eller minskat på den nya operativ system versionen. Skriv bords analys beräknar den här procent andelen för följande uppsättningar:  

  - **Efter uppdatering**: enheter som har uppdaterats till mål-OS-versionen som anges i distributions planen. För att minska antalet till gångar med otillräckliga data samlar Skriv bords analys in dessa data för alla dina uppdaterade enheter. Den här uppsättningen innehåller enheter som inte finns i distributions planen.  

  - **Före uppdateringen**: enheter som har en tidigare operativ system version än vad som anges i distributions planen. Listan innehåller inte enheter som kör Windows 7.  

  - **Kommersiellt Genomsnittligt**antal krascher i genomsnitt (genomsnittligt) för alla kommersiella enheter. Detta genomsnitt beräknas i *alla* versioner av appen. Om din version visar en krasch takt över det kommersiella genomsnittet kan det finnas en mer stabil version.  

- **% Sessioner med krascher**: liknar föregående, men räknar procent andelen sessioner med krascher under de senaste två veckorna.  

För att fastställa hälso status för en app kräver Desktop Analytics data från minst 20 enheter. Annars rapporterar den **inte tillräckligt med data** för appen. Tjänsten beräknar hälso status baserat på *sessionens krasch hastighet* från dessa enheter. Enhetens krasch pris tillhandahålls enbart för information. Den används inte i hälso status beräkningen.

### <a name="usage"></a>Användning

<!-- 5533890 -->

- **Aktiva enheter**: det här värdet är antalet enheter där en användare startade den valda appen under de senaste två veckorna. Den baseras på enheter i den valda distributions planen som kör mål versionen av Windows 10.

- **Sessioner**: det här värdet är det totala antalet gånger som en användare startade den valda appen i mål versionen av Windows.

### <a name="additional-tabs"></a>Ytterligare flikar

Längst ned på sidan information om appar kan följande tre flikar hjälpa dig att felsöka:

- **Andra versioner**: en lista över alternativa versioner av den här appen. För varje version visas de relativa ändringarna av krasch priserna i din organisation och det kommersiella genomsnittet. Om du hittar en senare version av appen med lägre krasch frekvens kan det hjälpa att uppdatera appen.  

    Den visar även om versionen har avancerade insikter. Mer information finns i [kompatibilitetskontroll](compat-assessment.md).  

- **Vanligaste problem**: en lista över de vanligaste fel-ID: na med instans antal. Ett felID identifierar stack spårningen som är associerad med kraschen. Du kan använda det här ID: t när du anropar leverantören av appen för support.  

- **Senaste krascher**: en lista över enheter där appen nyligen kraschade. Du kan filtrera efter ID för Miss lyckas och andra kriterier. Använd den här informationen för att felsöka problemet genom att samla in loggar eller prova korrigeringar på vissa enheter innan du testar en bredare distribution.  

Om du hittar en allvarlig hälso analys som du inte kan åtgärda kan du ändra appens **uppgraderings beslut** till att **det inte går**att göra. Den här åtgärden förhindrar framtida distribution av uppdateringen till enheter med den här till gången.

## <a name="see-also"></a>Se även

- [Kompatibilitetskontroll i Desktop Analytics](compat-assessment.md)  

- [Så här distribuerar du till produktion med Desktop Analytics](deploy-prod.md)  
