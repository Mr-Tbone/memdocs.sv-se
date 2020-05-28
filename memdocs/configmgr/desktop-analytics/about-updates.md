---
title: Uppdateringar i Skriv bords analys
titleSuffix: Configuration Manager
description: Lär dig mer om säkerhets-och funktions uppdateringar i Desktop Analytics.
ms.date: 04/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 14ae894c-26fb-4fe3-b51d-e80700122df4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 1c79db413f8e37424b84d98d51fb584d168e3819
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268937"
---
# <a name="updates-in-desktop-analytics"></a>Uppdateringar i Skriv bords analys

Visa status för säkerhets-och funktions uppdateringar i Skriv bords analys portalen. Välj de här noderna i övervaknings gruppen i huvud menyn för Skriv bords analys. Dessa noder ger dig insikter om status för dessa uppdateringar i din miljö.


## <a name="security-updates"></a>Säkerhetsuppdateringar

Om du vill granska den aktuella statusen för säkerhets uppdateringar väljer du **säkerhets uppdateringar** i **övervaknings** avsnittet i Skriv bords analys:

![Noden säkerhets uppdateringar i Skriv bords analys](media/security-updates.png)

I den här vyn sammanfattas *säkerhets* uppdateringar för enheter som kör Windows 10. Enheter i stapeldiagrammet kategoriseras enligt följande etiketter:

#### <a name="latest"></a>Nya

Enheterna kör den senaste säkerhets uppdateringen för den versionen och kanalen.

#### <a name="latest-1"></a>Senaste-1

Enheter kör en säkerhets uppdatering en version som är äldre än den senaste tillgängliga uppdateringen på den kanalen.

#### <a name="older"></a>Äldre

Enheter kör en säkerhets uppdatering som är äldre än den senaste-1.

#### <a name="not-measured"></a>Inte uppmätt

Desktop Analytics har inte utvärderat enheten. Detta tillstånd inkluderar enheter som kör Windows 7-, Windows 8,1-eller Windows 10-enheter som är registrerade för Windows Insider program.  

Om du vill se antagande trender för säkerhets uppdateringar väljer du **Visa mer** för en speciell version av Windows. Det staplade ytdiagram kategoriserar enheter efter säkerhets uppdateringen de har installerat med tiden.

Om du vill granska distributions status för säkerhets uppdateringar väljer du **Visa alla**. I den här vyn visas enheter i följande kategorier:

- Inte startad
- Pågår
- Slutförd
- Kräver åtgärd – enheter (sorterat efter enhets namn)
- Kräver åtgärds problem (sorteras efter typ av ärende)

Om du vill visa enheter med ny information som tjänsten fortfarande bearbetar väljer du **Visa aktuella data**. Skriv bords analys visar den här informationen efter nästa fullständiga data uppdatering.

  > [!IMPORTANT]
  > Alternativet Skriv bords analys för att **Visa senaste data** är föråldrat. Den här åtgärden kommer att tas bort i en framtida version av Desktop Analytics-tjänsten. Mer information finns i [föråldrade funktioner](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).<!--7080949-->  

## <a name="feature-updates"></a>Funktionsuppdateringar

Om du vill granska den aktuella statusen för funktions uppdateringar väljer du **funktions uppdateringar** i **övervaknings** avsnittet i Skriv bords analys:

![Noden funktions uppdateringar i Skriv bords analys](media/feature-updates.png)

I den här vyn sammanfattas *funktions* uppdateringar för enheter som kör Windows 10.

Mer information om service perioder finns i [fakta blad för Windows-livscykel](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet).  

Enheter i stapeldiagrammet kategoriseras enligt följande etiketter:

#### <a name="in-service"></a>I tjänst

Enheterna kör den senaste funktions uppdateringen för den versionen och kanalen.  

#### <a name="near-end-of-service"></a>Nära tjänstens slut

Enheter kör en funktions uppdatering som ligger inom 90 dagar efter att tjänsten har nått sin slut.

#### <a name="end-of-service"></a>Tjänstens slut

Enheter kör en funktions uppdatering som har passerat tjänst datumets slut. Dessa datum är särskilt aktuella för Enterprise-och Education-versioner av Windows. De gäller inte för hem-, Pro-, Pro-utbildning eller Pro för arbets Stations versioner. Mer information finns i [faktabladet om Windows livscykel](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)

#### <a name="not-measured"></a>Inte uppmätt

Desktop Analytics har inte utvärderat enheten. Detta tillstånd inkluderar enheter som kör Windows 7-, Windows 8,1-eller Windows 10-enheter som är registrerade för Windows Insider program.

Välj panelen för att se antagande trender för funktions uppdateringar. Det staplade ytdiagram kategoriserar enheter efter den funktions uppdatering de har installerat med tiden.

## <a name="next-steps"></a>Nästa steg

- [Lär dig mer om Desktop Analytics-till gångar](about-assets.md): enheter, driv rutiner och appar  

- [Lär dig mer om distributions planer](about-deployment-plans.md)  
