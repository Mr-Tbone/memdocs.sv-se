---
title: Installationsreferens
titleSuffix: Configuration Manager
description: Granska den här referensen för att hjälpa dig att förbereda installationen av en Configuration Manager plats eller hierarki.
ms.date: 04/18/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cdb9fb0c-0912-41e4-b427-f40620971763
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d948452da54a41e35095b01cb0e942e02a7a597f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718072"
---
# <a name="reference-for-configuration-manager-setup"></a>Referens för Configuration Manager-installationen

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager-installationen innehåller länkar till flera avsnitt som beskrivs i följande avsnitt. Informationen som presenteras här kan hjälpa dig att förbereda för att installera en Configuration Manager plats eller hierarki och hjälper dig att förbereda dig för några av de beslut som du måste fatta under installationen.  


##  <a name="before-you-begin"></a><a name="bkmk_start"></a>Innan du börjar  
Innan du installerar nya Configuration Manager-platser bör du kontrol lera att du har granskat följande information, som kan hjälpa dig att ställa in fasen för en lyckad distributions design:  

-   [Grunder i Configuration Manager](../../../../core/understand/fundamentals.md)  
-   [Planera för Configuration Manager infrastruktur](../../../plan-design/network/configure-firewalls-ports-domains.md)  
-   [Förbered för att installera Configuration Manager-platser](prepare-to-install-sites.md)  

##  <a name="assess-server-readiness"></a><a name="bkmk_assess"></a>Utvärdera serverns beredskap  
Innan du påbörjar installationen av en ny plats måste du kontrol lera att plats servern och de fjärranslutna plats system servrarna som du planerar att använda för platsen (till exempel den server som är värd för plats databasen) uppfyller alla nödvändiga konfigurationer. Följande avsnitt i dokumentations biblioteket kan hjälpa dig:  

-   [Konfigurationer som stöds för Configuration Manager](../../../../core/plan-design/configs/supported-configurations.md)  
-   [Krav kontroll](prerequisite-checker.md)  

##  <a name="clients-for-additional-operating-systems"></a><a name="bkmk_Addclients"></a>Klienter för ytterligare operativ system  
Du kan hämta klient program varan för Configuration Manager från Microsoft Download Center för följande operativ system:  

- macOS (Apple)
- UNIX
- Linux

Använd följande länkar för att hämta klienter för den version av Configuration Manager som du använder:  

- [Microsoft Endpoint Configuration Manager-macOS-klient (64-bitars)](https://www.microsoft.com/download/details.aspx?id=100850)

- [Microsoft Configuration Manager-klienter för ytterligare operativ system](https://www.microsoft.com/download/details.aspx?id=47719)

##  <a name="usage-data-levels-and-settings"></a><a name="bkmk_usage"></a> Nivåer för dataanvändning och inställningar  
När du installerar din första Configuration Manager-plats installerar och konfigurerar Configuration Manager automatiskt en ny plats system roll, **tjänst anslutnings punkten**, på plats servern. Tjänst anslutnings punkten har följande standardinställningar:  

-   **Onlineläge** (offline-läge är också tillgängligt)  
-   **Förbättrad** data insamlings nivå (två andra data insamlings nivåer, Basic och full, är också tillgängliga)  

När tjänst anslutnings punktens plats system roll är online kan Microsoft automatiskt samla in diagnostik-och användnings information via Internet. Information som samlas in hjälper oss att:  

-   Identifiera och felsöka problem  
-   Förbättra våra produkter och tjänster  
-   Identifiera uppdateringar för Configuration Manager som gäller för den version av Configuration Manager som du använder  

### <a name="levels-of-data-collection"></a>Nivåer för data insamling  
Data insamling innehåller följande tre nivåer:

-   **Basic** innehåller information om installation och uppgradering, t. ex. antalet webbplatser och vilka Configuration Manager funktioner som är aktiverade. Ingen personligt identifierbar information överförs.  

-   **Förbättrad** omfattar data i inställningen grundläggande nivå, plus data om hierarkin, hur varje funktion används (frekvens och varaktighet) och förbättrad diagnostikinformation, t. ex. minnes tillstånd för servern när ett system eller en app kraschar. Inga personligt identifierbara data överförs.  

-   **Fullständig omfattar alla** data i inställningarna grundläggande och utökad nivå, och skickar även avancerad diagnostikinformation, t. ex. systemfiler och ögonblicks bilder av minnet. Det här alternativet kan innehålla personligt identifierbar information, men vi kommer inte att använda informationen för att identifiera eller kontakta dig eller för att rikta in dig på annonsering.  

Mer information, inklusive information om de uppgifter som samlas in av varje nivå, finns i [diagnostik-och användnings data för Configuration Manager](../../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).  

Om du vill visa Configuration Manager sekretess policyn på raden går du [https://go.microsoft.com/fwlink/?LinkID=626527](https://go.microsoft.com/fwlink/?LinkID=626527)till.
